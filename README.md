PaxosCluster
============

A framework for distributed applications. Implements the Multi-Paxos protocol. Written in Go 1.2. (For cross compilation, use Go 1.5+, I'm using 1.5.4)

Video demo: http://www.youtube.com/watch?v=jyel-iADuUU

Full spec: https://skydrive.live.com/redir?resid=55025043B9B81FAF%215025

Video explaining the protocol: http://www.youtube.com/watch?v=JEpsBg0AO6o

## Build

1. Download & install Go version 1.X from https://golang.org/dl/
2. Clone this repo into $GOPATH/src/github/paxoscluster
3. Open a terminal in the paxoscluster directory and run `go build`

## Run on local machine

This mode of operation spins up five goroutines on your local machine, each acting as an independent process running the Paxos protocol (with replica IDs 1-5) listening on ports 10000-10004.
You can then type arbitrary text into the console, and upon pressing enter the text will be used as a proposed value for the next available multi-paxos slot.
The replicas persist their log to disk in the `coldstorage` directory.
All requests are sent to the proposer with ID 5, and fault injection is not supported.

To run in this mode, execute `go run simplecluster.go runlocal`, or after building execute `PaxosCluster runlocal`.
Exit using ctrl+c.
You can change the ports on which the processes listen by editing the `coldstorage/peers.csv` file.

## Run on cluster of machines

To run this mode, 

1. Update peers.csv file, include all the local address of machines in the network
2. execute `go build` to build for current system
3. execute `env GOOS=windows GOARCH=amd64 go build` to build for Windows
4. execute `env GOOS=darwin GOARCH=amd64 go build` to build for MacOS
5. execute `env GOOS=linux GOARCH=amd64 go build` to build for Linux

> Wait for all the devices to establish connections first before sending messages.