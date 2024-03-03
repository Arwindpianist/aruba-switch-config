
---

# Aruba Switch Configuration Guide

This guide provides step-by-step instructions for configuring Aruba Switches version 10.13.0001.

## Initial Setup

1. **Hostname Configuration:**
   ```
   hostname <hostname>
   ```
   Replace `<hostname>` with the desired name for your switch. This command sets the hostname of the switch to the specified value.

2. **Management IP Address Configuration:**
   ```
   interface mgmt
   ip static x.x.x.x/x
   default-gateway x.x.x.x
   ```
   Replace `x.x.x.x/x` with the desired IP address and subnet mask for the management interface of the switch. Also, replace `x.x.x.x` with the IP address of the default gateway.

## VLAN Configuration

1. **Creating VLANs:**
   ```
   interface vlan <vlan>
   description <description>
   ```
   Before proceeding with interface configurations, create all required VLANs using the above command. Replace `<vlan>` with the VLAN ID and `<description>` with a brief description of the VLAN. This command creates a VLAN with the specified ID and description.

## Persona Configuration

1. **Creating a Persona:**
   ```
   interface persona <persona-name>
   no shutdown
   no routing
   vlan access <vlan>
   exit
   ```
   Replace `<persona-name>` with the name of the persona and `<vlan>` with the VLAN ID. This command creates a persona and assigns it to the specified VLAN, disabling routing on that interface. You can create multiple personas if certain interfaces require different configurations. Feel free to add other configurations onto this persona as it will be copied onto the interfaces you select.

2. **Copying Persona Configuration to Interfaces:**
   ```
   interface 1/1/1-1/1/28
   persona custom <persona-name> attach
   exit
   ```
   Replace `<persona-name>` with the name of the persona you previously created. This command copies the configuration defined in the specified persona to the interfaces within the specified range.

## Trunk Persona Configuration

1. **Configuring Trunk Persona:**
   ```
   interface persona <trunk-persona-name>
   no shutdown
   no routing
   vlan trunk native <vlan>
   vlan trunk allowed all
   exit
   ```
   Replace `<trunk-persona-name>` with the name of the trunk persona and `<vlan>` with the native VLAN ID. This command creates a trunk persona with the specified configurations.

2. **Copying Trunk Persona Configuration to Interfaces:**
   ```
   interface <x/x/x or x/x/x-x/x/x>
   persona custom <trunk-persona-name> attach
   exit
   ```
   Replace `<x/x/x or x/x/x-x/x/x>` with the range of interfaces where the trunk persona configuration should be applied. This command copies the trunk persona configuration to the specified interfaces.

## Security Configuration

1. **Setting Passwords:**
   ```
   user admin password ciphertext <password>
   ```
   Set a password for the admin account. Replace `<password>` with the ciphertext value of the desired password.

---

This README provides a basic overview of configuring Aruba Switches version 10.13.0001. For detailed instructions and additional configurations, refer to the [official Aruba documentation](https://www.arubanetworks.com/techdocs/AOS-CX/10.13/PDF/fundamentals_6200.pdf) or consult with your network administrator.

---

Best of luck.
-arwin