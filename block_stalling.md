# Stalling in Bitcoin Core

During IBD or fully synced node, we are not advancing the current chain tip then the process is known as stalling. This can be caused by slow or 
unresponsive peers. 

### Bitcoin Core stalling mechanism detection -> [here](https://github.com/bitcoin/bitcoin/blob/638a4c0bd8b53766faeb437244b2aae4eed28dcf/src/net_processing.cpp#L5851)
We're gonna detect if a peer is delaying block or header downloads that will hinder the sync up time.

When the block download windows cannot move, the stalling occurs. During normal steady state, the download window should be much larger than the to-be-downloaded set of blocks, so disconnection
should only happen during initial block download.

`BLOCK_STALLING_TIMEOUT_DEFAULT` - is a constant which defines the default time for stalling before the peer is disconnected, which is `2LL` i.e. 2 secs.
Basically, if the block download window is not advanced within this timeout(`BLOCK_STALLING_TIMEOUT_DEFAULT`) then the peer is disconnected
to prioritize faster peers. 

After the node has figured the stalled peer from the check [`if (state.m_stalling_since.count() && state.m_stalling_since < current_time - stalling_timeout)`](https://github.com/bitcoin/bitcoin/blob/638a4c0bd8b53766faeb437244b2aae4eed28dcf/src/net_processing.cpp#L5853C9-L5853C104),
after that node will flag `fDisconnect` to `true` which will cause the disconnection to the peer next time [DisconnectNode()](https://github.com/bitcoin/bitcoin/blob/638a4c0bd8b53766faeb437244b2aae4eed28dcf/src/net.cpp#L3662) runs.
After disconnecting a peer, we make sure that we don't disconnect next peer where our bandwidth might be the cause, so for that case we increase
the timeout to double(4 secs, 8 secs) or `BLOCK_STALLING_TIMEOUT_MAX`(maximum timeout for block stalling, 64 secs) whichever is lower.


[#30251](https://github.com/bitcoin/bitcoin/pull/32051) : to-do



