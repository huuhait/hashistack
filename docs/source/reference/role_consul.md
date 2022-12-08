
```{include} ../../../roles/consul/README.md
```

## Defaults

```

consul_datacenter_name: "{{ hs_workspace }}"
consul_version: "1.13.1-1"

consul_connect_token: ~
consul_inventory_masters_group: "{{ consul_datacenter_name }}_masters"
consul_inventory_minions_group: "{{ consul_datacenter_name }}_minions"

consul_connect_root_pki_path: "connect_root"
consul_connect_intermediate_pki_path: "connect_inter"

consul_vault_address: "https://{{ groups[consul_inventory_masters_group][0] }}:8200"
consul_api_port: "8501"
consul_address: "https://127.0.0.1:{{ consul_api_port }}"

consul_server: "{{ __consul_is_master | ternary('true', 'false') }}"
consul_server_name: "{{ inventory_hostname }}"
consul_bootstrap_expect: 3
consul_node_name: >-
  {{ inventory_hostname | regex_replace('\.', '-') }}

consul_advertise_addr: "{{ ansible_default_ipv4.address }}"
consul_use_custom_ca: true
consul_acl_default_policy: deny
consul_acl_auto_encrypt_token: ~
consul_ca_certificate_dir: "/usr/local/share/ca-certificates"
consul_ca_certificate: "/etc/ssl/certs/ca-certificates.crt"
consul_local_secrets_dir: "{{ hs_workspace_secrets_dir }}"
consul_node_cert: ~
consul_node_cert_private_key: ~
consul_node_cert_fullchain: ~
consul_master_partners: >-
  {{
    groups[consul_inventory_masters_group]
    | difference([inventory_hostname])
  }}