Sample Linux Role for OpenSwitch OPX
=============================================

This sample role facilitates the configuration of Quality Of Service(QOS) parameters using CPS API in OPX.
The ansible-role-opx-qos role requires an SSH connection for connectivity to a Dell EMC OPX device.

Installation
------------

    ansible-galaxy install open-switch.opx-qos

Role Variables
--------------

- Role is abstracted using the *ansible_net_os_name* variable that needs the value "openswitch".
- Any role variable with a corresponding state variable set to absent negates the configuration of that variable
- Setting an empty value for any variable negates the corresponding configuration
- Variables and values are case-sensitive

**ansible-role-opx-qos keys**

| Key        | Type                      | Description                                             |
|------------|---------------------------|---------------------------------------------------------|
| ``opx_qos`` | list        | Configures create/delete QOS parameters (see `opx_qos.*`)   |
| ``opx_qos.qos_wred_attr_data``| dictionary  | Configures the WRED entry                                  |
| ``opx_qos.qos_wred_attr_data.green-enable``| integer  | Enables/disables the green WRED entry; 1 for enable and 0 for disable; value is set to 0 by default if disabled |
| ``opx_qos.qos_wred_attr_data.green-min-threshold``| integer | Minimum threshold in bytes after which packets will be dropped based on the drop probability |
| ``opx_qos.qos_wred_attr_data.green-max-threshold``| integer | Maximum threshold in bytes after which packets will be tail dropped |
| ``opx_qos.qos_wred_attr_data.green-drop-probability``| integer |Percentage probability with which packets will be dropped when minimum threshold is reached; value is set to 100 by default if unspecified |
| ``opx_qos.qos_wred_attr_data.yellow-enable``| integer  | Enables/disables the yellow WRED entry; 1 for enable and 0 for disable; value is set to 0 by default if unspecified |
| ``opx_qos.qos_wred_attr_data.yellow-min-threshold``| integer | Minimum threshold in bytes after which packets will be dropped based on the drop probability |
| ``opx_qos.qos_wred_attr_data.yellow-max-threshold``| integer | Maximum threshold in bytes after which packets will be tail dropped |
| ``opx_qos.qos_wred_attr_data.yellow-drop-probability``| integer | Percentage probability with which packets will be dropped when minimum threshold is reached; value is set to 100 by default if unspecified |
| ``opx_qos.qos_wred_attr_data.weight``| integer | Average queue size depends on the previous average as well as the current size of the queue; weight indicates the importance of the previous average queue length compared to the current queue size; value is set to 0 by default if unspecified |
| ``opx_qos.qos_wred_attr_data.npu-id-list``| list| List of NPU Ids |
| ``opx_qos.qos__scheduler``| dictionary  | Configures the scheduler profile entry |
| ``opx_qos.qos__scheduler.algorithm``| integer | Parameter gets the type of scheduling algorithm; 1 for strict priority, 2 for WDD, and 3 for WDRR; value is set to 3 (WDRR) by default if unspecified |
| ``opx_qos.qos__scheduler.weight``| integer | Scheduling weight |
| ``opx_qos.qos__scheduler.meter-type``| integer | Parameter get the meter type; 1 for packet and 2 for byte |
| ``opx_qos.qos__scheduler.min-rate``| long  | Guaranteed bandwidth shape rate (bytes/sec or PPS) |
| ``opx_qos.qos__scheduler.min-burst``| long  | Guaranteed burst for bandwidth shape rate (bytes or packets) |
| ``opx_qos.qos__scheduler.max-rate``| long  | Maximum bandwidth shape rate (bytes/sec or PPS) |
| ``opx_qos.qos__scheduler.max-burst``| long  | Maximum burst for bandwidth shape rate (bytes or packets) |
| ``opx_qos.qos_dscp_map_id`` | dictionary  | Configures attibutes to be set in CPS for DSCP map ID entry |
| ``opx_qos.qos_dscp_map_id.name``| string| Optional user-provided name for the map |
| ``opx_qos.qos_dscp_map_entry`` | dictionary  | Configures attibutes to be set in CPS for DSCP map entry |
| ``opx_qos.qos_dscp_map_entry.tc``| integer | Traffic class |
| ``opx_qos.qos_dscp_map_entry.color`` | integer | Packet color that given dscp is mapped to |
 | ``opx_qos.qos_dscp_map_entry.dscp``  | integer | Incoming DSCP value |
| ``opx_qos.qos_tc_map_id`` | dictionary  | Configures attibutes to be set in CPS for traffic class map ID entry |
| ``opx_qos.qos_tc_map_id.name``| string| Optional user-provided name for the map |
| ``opx_qos.qos_tc_map_entry`` | dictionary  | Configures attibutes to be set in CPS traffic class map entry |
| ``opx_qos.qos_tc_map_entry.tc``| integer | Traffic class |
| ``opx_qos.qos_tc_map_entry.color`` | integer | Packet color |
| ``opx_qos.qos_tc_map_entry.dscp`` | integer | Egress DSCP value for this traffic class and color |
| ``opx_qos.qos_policer_meter`` | dictionary  | Configures attibutes to be set in CPS meter entry |
| ``opx_qos.qos_policer_meter.peak-rate``| long | Peak rate in byte-per-second or packets; only valid for two-rate tri-color meter |
| ``opx_qos.qos_policer_meter.type`` | integer | Parameter get the meter type; 1 for packet and 2 for byte |
| ``opx_qos.qos_policer_meter.mode`` | integer | Meter mode type; 1 for single-rate, 2 for two-rate, 3 for two-color, and 4 for storm control |
| ``opx_qos.qos_queue_set_data``| dictionary  | Configures attibutes to be set in CPS for queue entry |
| ``opx_qos.qos_queue_set_data.queue-number`` | integer| Locally unique ID within a port and a specific queue type |
| ``opx_qos.qos_queue_set_data.type`` | integer | Data type; 1 for UNICAST queue 2 for multicast queue | 
| ``opx_qos.qos_queue_set_data.port-id`` | integer | Port number |
| ``opx_qos.qos_queue_set_data.buffer-profile-id``  | integer | Buffer profile ID |
| ``opx_qos.qos_queue_unset_data``| dictionary  | Configures attibutes to be unset in the CPS for queue entry |
| ``opx_qos.qos_queue_unset_data.queue-number`` | integer| Locally unique ID within a port and a specific queue type |
| ``opx_qos.qos_queue_unset_data.type`` | integer | Unset data type; 1 for Unicast queue and 2 for Multicast queue | 
| ``opx_qos.qos_queue_unset_data.port-id`` | integer | Port number |
| ``opx_qos.qos_queue_unset_data.buffer-profile-id``  | Integer | Buffer profile ID |
| ``opx_qos.qos_queue_unset_data.wred``   | integer | WRED profile ID |
| ``opx_qos.qos_ing_port``| dictionary  | Configures attibutes to be set in the CPS for port ingress entry |
| ``opx_qos.qos_ing_port.port-id`` | integer | port number |
| ``opx_qos.qos_egr_port``| dictionary  | Configures attibutes to be set in the CPS for port egress entry |
| ``opx_qos.qos_egr_port.port-id`` | integer | Port number |

> **NOTE**: Asterisk (\*) denotes the default value if none is specified.

Dependencies
------------

The *ansible-role-opx-qos* role is built on modules included in the core Ansible code. These modules were added in Ansible version 2.4.0.

Example playbook
----------------

This example uses the *open-switch.ansible-role-opx-qos* role to setup QOS using CPS Generic module. It creates a *hosts* file with the switch details and corresponding variables. The hosts file should define the *ansible_net_os_name* variable "openswitch".

It writes a simple playbook that only references the *ansible-role-opx-qos* role. By including the role, you automatically get access to all of the tasks to configure QoS features.


**Sample hosts file**

    leaf1 ansible_host= <ip_address> ansible_net_os_name="openswitch" ansible_ssh_user=<login> ansible_ssh_pass=<pwd>
    
**Sample host_vars/leaf1**
 
	opx_qos:
	  - operation: create
	    qos_wred_attr_data:
	      green-enable: 1
	      green-min-threshold: 10
	      green-max-threshold: 20
	      green-drop-probability: 1
	      yellow-enable: 1
	      yellow-min-threshold: 10
	      yellow-max-threshold: 20
	      yellow-drop-probability: 3
	      weight: 8
	      ecn-enable: 1
	      npu-id-list: [0]
	    qos_scheduler:
	      name: strict priority
	      algorithm: 1
	      weight: 2
	      meter-type: 1
	      min-rate: 256
	      min-burst: 300
	      max-rate: 1000
	      max-burst: 1200
	    qos_dscp_map_id:
	      switch-id: 0
	      name: dscp_map
	    qos_dscp_map_entry:
	      base-qos/dscp-to-tc-color-map/entry/tc: 0
	      base-qos/dscp-to-tc-color-map/entry/color: 1
	      base-qos/dscp-to-tc-color-map/entry/dscp: 40
	    qos_tc_map_id:
	      switch-id: 0
	      name: dscp_map
	    qos_tc_map_entry:
	      base-qos/tc-color-to-dscp-map/entry/tc: 0
	      base-qos/tc-color-to-dscp-map/entry/color: 1
	      base-qos/tc-color-to-dscp-map/entry/dscp: 40
	    qos_policer_meter:
	      type: 1
	      peak-rate: 10
	      mode: 4
	  - operation: set
	    qos_queue_set_data:
	      port-id: 17
	      queue-number: 4
	      type: 2
	      buffer-profile-id: 4
	    qos_queue_unset_data:
	      port-id: 17
	      queue-number: 4
	      type: 2
	      buffer-profile-id: 0
	      wred-id: 0
	    qos_ing_port:
	      port-id: 16
	    qos_egr_port:
	      port-id: 17
	  - operation: delete
	    qos_wred_attr_data:

	 
**Simple playbook to setup system - leaf.yaml**

    - hosts: leaf1
      roles:
         - { role: open-switch.ansible-role-opx-qos, when: ansible_net_os_name is defined and ansible_net_os_name == "openswitch" }


**Run**

    ansible-playbook -i hosts leaf.yaml
    
(c) 2018 Dell EMC
