========
Module 1
========

.. contents:: Table of Contents

1. Instructions for using the Translator Application
----------------------------------------------------

1. Open a web browser (Chrome) 
2. Go to the URL http://localhost:5000
3. If you **DO NOT** see the web application on your screen, please use the keys **Ctrl-Alt-T** on your keyboard to open a terminal window or open it using the terminal icon on your desktop. Then, copy and paste the following commands into the terminal and press Enter:

   .. code-block:: bash

      docker rm -fv $(docker ps -aq)
      sudo lsof -i :5000 
      sudo kill -9 <Enter PID>
      docker-compose up

4. Take a moment to hover over the various elements of the translator application. Tooltips will appear with useful information and guidance to help you utilize the application
5. Please select **my_ACI_playbook.yml** which is in the **Module1** folder of the **DEVWKS-2302** directory
6. The contents of the playbook are as follows:

  .. code-block:: yaml

    ---
    - name: my_ACI_playbook
      hosts: aci
      gather_facts: no
      tasks:

        - name: Set vars
          ansible.builtin.set_fact: 
            aci_info: &aci_info
              host: "{{ ansible_host }}"
              username: "{{ ansible_user }}"
              password: "{{ ansible_password }}"
              validate_certs: '{{ validate_certs | default(false) }}'
              use_ssl: '{{ use_ssl | default(true) }}'
              output_level: debug

        - name: Create a tenant
          cisco.aci.aci_tenant:
            <<: *aci_info 
            tenant: ansible_to_tf
            state: present

        - name: Create a VRF
          cisco.aci.aci_vrf: 
            <<: *aci_info
            tenant: ansible_to_tf
            vrf: l3outtest
            state: present

        - name: Create an L3Out
          cisco.aci.aci_l3out:
            <<: *aci_info
            tenant: ansible_to_tf
            l3out: l3-dmz-ex-1
            domain: l3outtest
            vrf: l3outtest
            route_control: export 
            state: present

        - name: Create a node profile
          cisco.aci.aci_l3out_logical_node_profile: 
            <<: *aci_info
            tenant: ansible_to_tf
            l3out: l3-dmz-ex-1
            logical_node: np1101
            state: present

        - name: Add a node
          cisco.aci.aci_l3out_logical_node:
            <<: *aci_info
            tenant: ansible_to_tf
            l3out: l3-dmz-ex-1
            logical_node: np1101
            pod_id: 1
            node_id: 1101
            router_id: 111.111.111.111
            state: present

        - name: Create a static route
          cisco.aci.aci_l3out_static_routes: 
            <<: *aci_info
            tenant: ansible_to_tf
            pod_id: 1
            node_id: 1101
            prefix: 192.168.8.0/24
            l3out: l3-dmz-ex-1
            logical_node: np1101
            state: present

        - name: Add a next hop to the static route
          cisco.aci.aci_l3out_static_routes_nexthop:
            <<: *aci_info
            tenant: ansible_to_tf
            l3out: l3-dmz-ex-1
            logical_node: np1101
            node_id: 1101
            pod_id: 1
            prefix: 192.168.8.0/24
            nexthop: 192.168.181.99
            state: present

6. Enter the APIC Host, APIC User ID and APIC Password prvoded in the handout
7. Click **Translate** button
8. After the translation is complete, click **Download Translated Files** button


2. Instructions for verifying the downloaded Terraform files
------------------------------------------------------------

1. Use the keys **Ctrl-Alt-T** on your keyboard to open a terminal window or open it using the terminal icon on your desktop.
2. Change the working directory to
2. Go to the URL http://localhost:3000
3. If you **DO NOT** see the web application on your screen, please use the keys **Ctrl-Alt-T** on your keyboard to open a terminal window or open it using the terminal icon on your desktop. Then, copy and paste the following commands into the terminal and press Enter:

   .. code-block:: bash

      docker rm -fv $(docker ps -aq)
      sudo lsof -i :5000 
      sudo kill -9 PID
      docker-compose up

4. Take a moment to hover over the various elements of the translator application. Tooltips will appear with useful information and guidance to help you utilize the application
5. Please select **my_ACI_playbook.yml** which is in the **Module1** folder of the **DEVWKS-2302** directory
6. Enter the APIC Host, APIC User ID and APIC Password in the handout
7. Click **Translate** button
8. After the translation is complete, click **Download Translated Files** button