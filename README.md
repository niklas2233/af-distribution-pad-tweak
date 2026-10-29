# Locker Distribution Pad (Abiotic Factor mod)

Makes the vanilla **Distribution Pad** also send items to the facility's pre-placed storage
(lockers, filing cabinets, toolboxes, fridges, desks, crates...), not only containers you built.
Like the vanilla pad, an item only goes to a container that already holds that item type.

## Why the vanilla pad skips them

`Deployed_DistributionPad.UpdateCompatibleContainers` only accepts containers with both
`CanItemTransport` and `FoundByPlayer` set. World-placed containers never get `FoundByPlayer`,
so the vanilla pad ignores them.

## What the mod does

`Deployed_Furniture_LockerDistPad` subclasses the vanilla pad and overrides
`UpdateCompatibleContainers`:

1. Toggles the container sphere's collision to force a fresh overlap check.
2. Takes every overlapping `Deployed_Container_ParentBP` with `CanItemTransport`.
3. Skips player corpses, loot spill bags and trader storage (incl. the autosalvager).
4. Adds the rest with the vanilla `AddContainer`.

`ItemTable_Craftables/distribution_pad` overrides the vanilla `distribution_pad` row so the
normal recipe places this pad. Pads already placed in a save stay vanilla until picked up and
placed again. The older standalone item (`NUVNS_LockerDistPad`) is kept, without a recipe, so
pads from earlier test builds still pick up correctly.

## Project

`LockerDistPadapQZ5/` is the Abiotic Factor Mod Editor project (open it from the editor's
mod browser). Built with the official Mod Editor (UE 5.4).
