# Adding More MikroTik Routers

## Option A: Folder Rule (recommended)
1. Put all MikroTik hosts into a folder (e.g., `Network/MikroTik`).
2. Attach one **Datasource Program** rule to the folder:
   ```bash
   $OMD_ROOT/local/share/check_mk/agents/special/agent_mikrotik \
     --host $HOSTADDRESS$ \
     --user 'cmk' \
     --password '***use Password Store***' \
     --timeout 8 \
     --if_filter 'ether,sfp,pppoe' \
     --wan_comments 'MainGW,RsrvGW,LastChanceGW' \
     --wan_if_map 'MainGW=ether7-Infolink,RsrvGW=pppoe-out-Flex,LastChanceGW=ether10-LTE' \
     --ping_target '77.88.8.8' \
     --ping_count 3
