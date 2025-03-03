Yeah, we all love em. Managers. But have you heard of:

# SHCMANAGER

This script helps manage your configuration files and related installations.

![Visual demo](https://github.com/jvaarala/shcmanager/blob/main/resources/visual_demo.gif)

## Prerequisites

```bash
git clone https://github.com/jvaarala/shcmanager.git
cd shcmanager
chmod +x shcmanager
```

The script uses a configuration file `.shcmanager.config` to set the working directory.
If the config file is not found, the script will prompt you to create one.

Example `.shcmanager.config`:

```
WORK_DIR=~/managed
```

This working directory will be used to store the managed configurations and plugins.

## Menu Navigation

When you run the script with install or uninstall, you will be presented with a menu to select the plugins you want to
manage.

- Use `k` to move the cursor up.
- Use `l` to move the cursor down.
- Use `i` to select or deselect an option.
- Use `q` to quit the menu.
- Press `Enter` to confirm your selection.

## Plugins

Core idea of `shcmanager` revolves around plugins. Plugins are used to manage configurations and installations of
different tools and applications.
Each plugin is a set of configuration and (un)installation steps that can be managed by the `shcmanager`.

Each plugin should have two functions: `install_<plugin_name>` and `uninstall_<plugin_name>`. These functions will be
called by the script to manage the plugin.  
The plugin name should be in lowercase and separated by underscores.

To add a new plugin, create a new file in the plugins directory and define the `install_<plugin_name>` and
`install_<plugin_name>` functions.

You can use the available adapters in plugins to perform common operations like clone a git repository, install brew
packages, or create symlinks.

### Create

There is also a `create` command to help you create a new plugin template.
To create a new plugin template, run:

```bash
./shcmanager create "foo bar"
```

This will create a new plugin template in the `plugins` directory with the name `foo_bar`. You can then add your
configurations and installation steps to the plugin.

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

### Example

To set up the IntelliJ IDEA keymap plugin, you can use the following commands:

1. Create the Plugin:
    ```bash
    ./shcmanager create zshrc
    ```
2. Edit the Plugin: Update the `plugins/zshrc` file with the appropriate install and uninstall functions:
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

