

Yeah, we all love 'em — managers. But have you heard of:
# SHCMANAGER

This script helps you manage configuration files and related installations.

![Visual demo](https://github.com/jvaarala/shcmanager/blob/main/resources/visual_demo.gif)

## Prerequisites

Clone the repository and set up the script:

```bash
git clone https://github.com/jvaarala/shcmanager.git
cd shcmanager
chmod +x shcmanager
```

The script uses a configuration file, `.shcmanager.config`, to define the working directory.  
If the config file is not found, the script will prompt you to create one.

### Example `.shcmanager.config`

```
WORK_DIR=~/managed
```

This working directory stores managed configurations and plugins.  
If you set `WORK_DIR` to a Git repository, you get automatic backups and version control for your configurations, making it easy to manage them across multiple machines.

## Menu Navigation

- Press `k` to move the cursor up.
- Press `l` to move the cursor down.
- Press `i` to select or deselect an option.
- Press `q` to quit the menu.
- Press `Enter` to confirm your selection.

## Plugins

The core idea of **hcmanager** revolves around **plugins**, which manage the configurations and installations of different tools and applications.  
Each plugin contains configuration and (un)installation steps that **shcmanager** can handle.

A plugin should define two functions:

- `install_<plugin_name>`
- `uninstall_<plugin_name>`

These functions are called by the script to manage the plugin.  
The plugin name should be in lowercase and use underscores (`_`) as separators.

### Creating a Plugin

To add a new plugin, create a file in the `plugins` directory and define the required `install_<plugin_name>` and `uninstall_<plugin_name>` functions.

You can use the available **adapters** to perform common tasks, such as:

- Cloning Git repositories
- Installing Homebrew packages
- Creating symlinks

### Using the `create` Command

`shcmanager` includes a `create` command to generate a new plugin template.  
To create a new plugin template, run:

```bash
./shcmanager create "foo bar"
```

This creates a new plugin template in the `plugins` directory as `foo_bar`.  
You can then add your configurations and installation steps to the plugin.

```bash
install_foo_bar() {
  echo ""
  echo "Installing foo_bar..."
}

uninstall_foo_bar() {
  echo ""
  echo "Uninstalling foo_bar..."
}
```

### Example: Managing `.zshrc`

You can create a plugin for each configuration file you want to manage.  
For example, to manage your `.zshrc` file:

1. **Create the Plugin:**
   ```bash
   ./shcmanager create zshrc
   ```
2. **Edit the Plugin:** Update `plugins/zshrc` with the following content:
   ```bash
   source "./adapters/symlink"

   install_zshrc() {
      echo ""
      echo "🔧 Setting up .zshrc configuration..."
      install_symlink "$HOME/managed/.zshrc" "$HOME/.zshrc"
   }

   uninstall_zshrc() {
      echo ""
      echo "🗑️ Removing .zshrc configuration..."
      uninstall_symlink "$HOME/managed/.zshrc" "$HOME/.zshrc"
   }
   ```
3. **Move the `.zshrc` file to the managed directory:**
   ```bash
   mv ~/.zshrc ~/managed/.zshrc
   ```
4. **Run the script:**
   ```bash
   ./shcmanager
   ```
   The `zshrc` plugin should now appear in the menu.

