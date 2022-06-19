# DMZAirdrop

The airdrop contract helps to airdrop tokens using merkle tree distributor.

 * **Claim** - Claim the designated amount of tokens from the distributor
 * claim (Claim) - Address of the receiver, amount to be redeemed and the leaves of the proof of the merkle tree for the address.
 * **RevokeOwnership** - Revoke the ownership transfer for any address.
 * **TransferOwnership** - Owner only transition to change owner. 
 * - new_owner (ByStr20) - new owner address
 * **AcceptOwnership** - New contract owner can accept the ownership transfer request.
 * **RedeemTokens** - Redeem leftover tokens by the admin from the distributor
 * - amount (Uint128) - Number of tokens to be redeemed


## Users Transitions
```Ocaml
contract DMZAirdrop
  Claim(claim: Claim)
```

## Owner Transitions
```Ocaml
contract DMZAirdrop
  TransferOwnership(new_owner: ByStr20)
  RevokeOwnership()
  AcceptOwnership()
  RedeemTokens(amount: Uint128)
```

## Callbacks
```Ocaml
contract DMZAirdrop
  RecipientAcceptTransfer(
  sender : ByStr20,
  recipient : ByStr20,
  amount : Uint128
  )
  TransferSuccessCallBack(
    sender : ByStr20,
    recipient : ByStr20,
    amount : Uint128
  )
```

## Constructor

 * init_owner - Owner of the contract.
 * token_contract - Contract address of the DMZ.
 * merkle_root - Merkle root of the airdrop generated by the backend

```Ocaml
contract DMZAirdrop
(
  token_contract : ByStr20,
  init_owner : ByStr20,
  merkle_root : ByStr32
)
```

## Errors

```Ocaml
contract DMZAirdrop
  type Error =
    | CodeNotOwner
    | CodeNotPendingOwner
    | CodePendingOwnerNotEmpty
    | CodeInvalidProof
    | CodeAlreadyClaimed
```

## Mutable fields

```Ocaml
contract DMZAirdrop
  field contract_owner : Option ByStr20 = Some {ByStr20} init_owner
  field pending_owner : Option ByStr20 = none

  field claimed_leafs : Map ByStr32 Bool = Emp ByStr32 Bool
```