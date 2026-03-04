# :cheese: CheesyScripts Documentation

**Official technical guides for our FiveM resources.**

Welcome to the central hub for **CheesyScripts**. This site provides installation steps, configuration guides, and export references for all our released products. Select a script from the sidebar to get started.

---

## :package: Global Requirements
Before installing any of our scripts, ensure your server meets these baseline requirements to avoid any "lactose intolerance" (script errors):

* **FXServer Artifacts:** Version `5848` or higher is recommended.
* **OneSync:** Enabled (Required for most modern networking features).
* **Database:** [oxmysql](https://github.com/overextended/oxmysql) .

---

## :rocket: Installation Flow
All CheesyScripts follow a standardized installation process:

1.  **Download:** Claim your asset from [FiveM Keymaster](https://keymaster.fivem.net/assets).
2.  **Placement:** Extract the folder into your `resources/` directory (e.g., `resources/[cheesy]`).
3.  **Config:** Edit the `config.lua` to match your framework (**ESX/QB/Standalone**).
4.  **Start:** Add `ensure [script_name]` to your `server.cfg`.

!!! success "Performance Monitoring"
    Our scripts are built with performance in mind. If you notice an idle MS higher than **0.01ms**, please check your configuration or open a support ticket.

---

## :handshake: Support & Links
If you encounter any issues not covered in these docs:

* **[Discord Support](https://discord.gg/SP5EYdJ8SG)** — Open a ticket for 1-on-1 assistance.
* **[Tebex Store](https://store.cheesyscripts.com/)** — Browse our latest premium releases.

---

### :bulb: Developer Note
> We use **Escrow** for our premium scripts, but we keep the `config.lua` and most `client/server` events open so you can still bridge them into your own custom frameworks.

**Stay Gouda.**