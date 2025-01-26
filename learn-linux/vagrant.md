[vagrant tutorial](https://devopscube.com/vagrant-tutorial-beginners/)

### Basic Commnads
| command-line | description |
| --- | --- |
| `vagrant init` | Initialize a Vagrant environment (creates a `Vagrantfile`) |
| `vagrant up` | Start and provision the VM |
| `vagrant ssh` | SSH into the VM |
| `vagrant halt` | vagrant halt |
| `vagrant reload` | Restart the VM |
| `vagrant destroy` | Destroy the VM (deletes all resources) |

### Provisioning Commands
| command-line | description |
| --- | --- |
| `vagrant provision` | Provision the VM (run provisioning scripts) |
| `vagrant reload --provision` | Reload and reprovision the VM |

### Status Information
| command-line | description |
| --- | --- |
| `vagrant status` | Check the status of the VM |
| `vagrant global-status` | List all VMs managed by Vagrant |
| `vagrant ssh-config` | Show SSH configuration for the VM |

### Networking
| command-line | description |
| --- | --- |
| `config.vm.network "forwarded_port", guest: 80, host: 8080` | Port forwarding (configure in Vagrantfile) |
| `config.vm.network "private_network", ip: "192.168.33.10"` | Private network (assign a static IP) |
| `config.vm.network "public_network"` | Public network (bridged mode) |

### Shared Foldes
| command-line | description |
| --- | --- |
| `config.vm.synced_folder "./host_folder", "/vagrant/guest_folder"` | Sync folders (configure in `Vagrantfile`) |

### Box Management
| command-line | description |
| --- | --- |
| `vagrant box add ubuntu/focal64` | Add a box (download a base image) |
| `vagrant box list` | List installed boxes |
| `vagrant box remove ubuntu/focal64` | Remove a box |
| `vagrant box update` | Update a box |

### Plugins
| command-line | description |
| --- | --- |
| `vagrant plugin install vagrant-vbguest` | Install a Vagrant plugin (e.g., vagrant-vbguest for VirtualBox Guest Additions) |
| `vagrant plugin list` | List installed plugins |
| `vagrant plugin uninstall vagrant-vbguest` | Uninstall a plugin |

### Snapshot Management
| command-line | description |
| --- | --- |
| `vagrant snapshot save my_snapshot` | Save the current state of the VM (requires vagrant-vbox-snapshot plugin) |
| `vagrant snapshot restore my_snapshot` | Restore a snapshot |
| `vagrant snapshot list` | List all snapshots |
| `vagrant snapshot delete my_snapshot` | Delete a snapshot |

### Debugging and Logs
| command-line | description |
| --- | --- |
| `vagrant up --debug` | Enable debug mode (useful for troubleshooting) |
| `vagrant log` | View Vagrant logs |

### Advanced Commands
| command-line | description |
| --- | --- |
| `vagrant suspend` | Suspend the VM (pause the VM state) |
| `vagrant resume` | Resume a suspended VM |
| `vagrant package` | Package the VM into a reusable box |
| `vagrant validate` | Validate the Vagrantfile syntax |

### Cleanup
| command-line | description |
| --- | --- |
| `vagrant box prune` | Remove unused boxes |
| `vagrant global-status --prune` | Remove all Vagrant-managed VMs |