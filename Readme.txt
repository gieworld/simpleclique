Create a Clique network

- Windows OS
- 3 Nodes

1. Start the first node as the bootnode

besu --data-path=data --genesis-file=..\cliqueGenesis.json --network-id 123 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-allowlist="*" --rpc-http-cors-origins="all"

2. Start Node-2

besu --data-path=data --genesis-file=..\cliqueGenesis.json --bootnodes=enode://d9a69cb84d31e0e5e2599bb05acb2316f48dd7d5964cf18d21f9acdb699a6332e112f607b073c4579dbca2eb31917f29e946dcf510fb0617bcc0727f237b11fd@127.0.0.1:30303 --network-id 123 --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546

3. Start Node-3

besu --data-path=data --genesis-file=..\cliqueGenesis.json --bootnodes=enode://d9a69cb84d31e0e5e2599bb05acb2316f48dd7d5964cf18d21f9acdb699a6332e112f607b073c4579dbca2eb31917f29e946dcf510fb0617bcc0727f237b11fd@127.0.0.1:30303 --network-id 123 --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,CLIQUE --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8547

4. Confirm the private network is working

Invoke-RestMethod -Method Post -Uri 'http://localhost:8545' -Body '{"jsonrpc":"2.0","method":"net_peerCount","params":[],"id":1}' -ContentType 'application/json'

The result confirms Node-1 has two peers (Node-2 and Node-3):

{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x2"
}

When finished using the private network, stop all nodes using ++ctrl+c++ in each terminal window.

