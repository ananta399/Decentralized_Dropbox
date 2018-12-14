### Decentralized DropBox
### README


A P2P decentralized Dropbox clone. Synchronizes files among multiple Linux devices, automatically handling file modification and renaming across devices.

TRACKER:

	Only one tracker should be running. It acts as the "server". Just compile the code using the "make" command on a Linux computer and run it using "./tracker". 

	Trackers fist creates a monitor thread to handle/disconnect all peers that havent sent heartbeat for a while.
	Then the tracker listens and accepts connections from peers, creating a new handshake thread for each peer.

	The handshake thread calls new_peer() that adds the peer to the table if table is not full.
	Then the thread keeps on receiving messages from the peer until it disconnects/timeouts. If the client sends "Close" message then this thread disconnects the client. If the client timeouts, then monitor thread disconnects the client.

PEER:

	Run these on all the peer computers you want to keep syncronized. Just compile the code using the "make" command on a Linux computer and run it using "./peer". 

	First it prompts to enter server name, which is the address of the tracker. This can for example be "flume.cs.dartmouth.edu"

	It connects to the tracker and sends a "REGISTER" signal and keeps on receiving data from the tracker.
	Meanwhile another thread "keepAlive" periodically sends heartbeat to the tracker.

	Peers automatically monitor the ./DROPBOX directory (relative to the directory your program is run from) and syncs it across all the other peers.
