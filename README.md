Yeah, we all love em. Managers. But have you heard of..
# SHCMANAGER

This script helps manage your configuration files and related installations.

![Visual demo](https://github.com/jvaarala/shcmanager/blob/main/resources/visual_demo.gif)

## Prerequisites


```bash
git clone https://github.com/jvaarala/shcmanager.git
cd shcmanager
chmod +x shcmanager
```


## Usage

The script supports three main operations: `install`, `uninstall`, and `create`.

### Install

To install the selected plugins and configurations, run:

```sh
./shcmanager install
```

### Uninstall
To uninstall the selected plugins and configurations, run:

```sh
./shcmanager uninstall
```

### Menu Navigation
When you run the script with install or uninstall, you will be presented with a menu to select the plugins you want to manage.  
- Use `k` to move the cursor up.
- Use `l` to move the cursor down.
- Use `i` to select or deselect an option.
- Use `q` to quit the menu.
- Press `Enter` to confirm your selection.


## Plugin Structure
To add a new plugin, create a new file in the plugins directory and define the install_<plugin_name> and uninstall_<plugin_name> functions.

Each plugin should have two functions: `install_<plugin_name>` and `uninstall_<plugin_name>`. These functions will be called by the script to manage the plugin.  
The plugin name should be in lowercase and separated by underscores.

### Create
There is also a `create` command to help you create a new plugin template.
To create a new plugin template, run:
```sh
./shcmanager create "foo bar"
```

This will create a new plugin template in the `plugins` directory with the name `foo_bar`. You can then add your configurations and installation steps to the plugin.

```sh
install_foo_bar() {
  echo "Installing contents of example plugin..."
  # Add installation commands here
}

uninstall_foo_bar() {
  echo "Uninstalling contents of example plugin..."
  # Add uninstallation commands here
}
```

