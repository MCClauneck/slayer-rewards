# SlayerRewards

**SlayerRewards** is a dynamic extension for the **MCEconomy** system. It allows server administrators to fully customize rewards for killing mobs, including monetary payouts, custom item drops, and visual feedback, all managed through an intuitive in-game GUI.

## 🌟 Features

* **In-Game GUI Editor:** Manage drops and rewards without ever leaving the game or touching config files manually.
* **Monetary Rewards:** Give players money for killing specific mobs. Supports fixed amounts or random ranges (e.g., 10-50 coins).
* **Multi-Currency Support:** Seamlessly switch rewards between different currency types (Coin, Copper, Silver, Gold).
* **Custom Item Drops:** Add any item (with custom enchants, names, or lore) to a mob's loot table using drag-and-drop.
* **Drop Chances:** Easily configure the percentage chance for every custom item drop.
* **Vanilla Drop Control:** Toggle whether the mob should still drop its default vanilla items (e.g., Rotten Flesh for Zombies) or only your custom loot.
* **Visual Feedback:** Displays a modern holographic pop-up (TextDisplay) at the mob's death location showing the amount earned.

## 📋 Requirements

* **Server Core:** Paper 1.21+ (Required for modern display entities).
* **Dependency:** MCEconomy.

## 🎮 Commands & Permissions

### Main Command
To manage mob rewards, use the following command:

```cmd
/slayerrewards edit <mob_type> [page]
```

* **<mob_type>:** The type of entity you want to edit (e.g., `zombie`, `skeleton`, `ender_dragon`). Supports tab-completion.
* **[page]:** (Optional) Jump to a specific page of the editor if you have many drops.

### Permissions
* `slayerrewards.admin`: Required to access the edit command and modify rewards.

---

## 🛠️ How it Works: The Editor GUI

When you run `/slayerrewards edit <mob>`, a custom inventory GUI opens. Here is how to use the interactive features:

### 1. Adding Custom Drops
* **Drag & Drop:** Simply drag items from your own inventory into the top section of the GUI.
* **Metadata:** The plugin saves the *exact* item, including enchantments, custom names, and lore.

### 2. Setting Drop Chances
* **Shift + Right Click:** To change the probability of an item dropping, hold Shift and Right-Click the item in the GUI.
* **Chat Input:** The GUI will close, and you will be prompted to type a number (0-100) in the chat.
* **Confirmation:** Once typed, the GUI reopens with the new percentage updated in the item's lore.

### 3. Monetary Rewards
* **Set Amount:** Click the **Paper** icon (bottom row). You will be prompted in chat to enter an amount.
* **Random Ranges:** You can enter a single number (e.g., `50`) or a range separated by a dash (e.g., `50-100`).
* **Currency Type:** Click the **Currency Head** icon (bottom row) to cycle through available currencies (Coin -> Copper -> Silver -> Gold).

### 4. Vanilla Drops Toggle
* **Toggle Switch:** Click the **Chest/Barrier** icon (bottom row).
    * **On:** Default vanilla drops (bones, flesh, etc.) will drop alongside your custom items.
    * **Off:** The mob will *only* drop the money and items you have configured.

### 5. Saving
* **Save Button:** Always click the **Save** icon (bottom right) before closing the inventory to ensure your changes are written to disk.

---

## 📂 Configuration Files

While the GUI handles most operations, the plugin generates configuration files for each mob you edit.

**Path:** `plugins/MCEconomy/extensions/SlayerRewards/mobs/<mobname>.yml`

### Example Configuration (`zombie.yml`)
If you prefer manual editing, the file structure looks like this:

```yaml
currency: "coin"           # The currency type given
amount: "10-20"            # Money given (supports ranges)
cancel_default_drops: true # If true, vanilla drops are disabled

item_drop:
  1:
    metadata: "..."        # Base64 string of the item stack
    amount: 1              # Stack size
    chance: 50.0           # 50% drop chance
  2:
    metadata: "..."
    amount: 2
    chance: 10.0           # 10% drop chance
```

## 💎 Visual Indicators

When a player kills a mob configured with **SlayerRewards**:

1. The money is immediately calculated and deposited into their account via MCEconomy.

2. A temporary Hologram appears floating above the corpse, displaying the amount earned (e.g., +50 COIN) in green text.
