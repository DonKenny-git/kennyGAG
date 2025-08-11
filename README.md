# kennyGAG – Roblox Pet Gifting (Duplicate on Gift)

This repo contains a single-file Roblox server script that manages pet inventories and a gifting system that duplicates pets for the recipient while the sender keeps the original.

## Files
- `Roblox/ServerScriptService/PetGiftingPure.server.lua` – pure server script (inventory, DataStore, gifting, remotes)
- `Roblox/StarterPlayer/StarterPlayerScripts/GiftTestUI.client.lua` – minimal client UI for testing (optional)

## Setup in Roblox Studio
1. Open your place in Roblox Studio.
2. In `ServerScriptService`, create a Script named `PetGiftingPure` and paste the contents of `Roblox/ServerScriptService/PetGiftingPure.server.lua`.
3. (Optional) In `StarterPlayer > StarterPlayerScripts`, create a LocalScript named `GiftTestUI` and paste `Roblox/StarterPlayer/StarterPlayerScripts/GiftTestUI.client.lua`.
4. Play Solo or start with 2 clients using Test tab.

## DataStore
- The script uses `DataStoreService` with store name `PetInventory_v1` and is protected with `pcall`.
- In Studio, to persist across sessions, enable: Game Settings > Security > "Enable Studio Access to API Services".
- If disabled, the script still runs; saves may be ignored by Studio.

## Remotes
The server creates these under `ReplicatedStorage/Remotes`:
- `GiftPet:InvokeServer(recipientUserId: number, petId: string)` – gifts a duplicate to `recipientUserId`.
- `GetInventory:InvokeServer()` – returns `{ ok, inventory }` for the caller.
- `SpawnTestPet:InvokeServer()` – adds a random test pet to the caller.

## Testing
- With 2 clients open, in the test UI enter the other client’s username.
- Click `+ Add Pet` to get a pet, then `Gift First Pet` to duplicate to the recipient.
- Cooldown and idempotency are enforced on the server.

## Switching to Transfer
- In `PetGiftingPure.server.lua`, change `DUPLICATE_ON_GIFT = true` to `false`.

## License
MIT 