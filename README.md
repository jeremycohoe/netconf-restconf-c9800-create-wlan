These NETCONF XML payloads can be used to create a WLAN on a Cisco Catalyst 9800 WLC running IOS XE 16.11

1. Create WLAN 

```
<rpc xmlns="urn:ietf:params:xml:ns:netconf:base:1.0" message-id="6">
<edit-config xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0">
   <target>
     <running/>
   </target>
   <test-option>test-then-set</test-option>
   <error-option>rollback-on-error</error-option>
   <config>
   <wlan-cfg-data xmlns="http://cisco.com/ns/yang/Cisco-IOS-XE-wireless-wlan-cfg">
     <wlan-cfg-entries>
       <wlan-cfg-entry>
         <profile-name>open</profile-name>
         <vap-id>4</vap-id>
         <security-wifi-sec>false</security-wifi-sec>
         <rsn-ie-enabled>false</rsn-ie-enabled>
         <rsn-cipher-suite-aes>false</rsn-cipher-suite-aes>
         <auth-key-mgmt-suite8021x>false</auth-key-mgmt-suite8021x>
         <client-session-timeout>1800</client-session-timeout>
         <id-data>
           <profile-name>open</profile-name>
           <ssid>open</ssid>
           <status>true</status>
         </id-data>
         <is-remote-lan>false</is-remote-lan>
       </wlan-cfg-entry>
     </wlan-cfg-entries>
   </wlan-cfg-data>
</config></edit-config></rpc>
```


2. Verify WLAN configuration

```
<rpc message-id="101" xmlns="urn:ietf:params:xml:ns:netconf:base:1.0">
  <get>
    <filter>
      <wlan-cfg-data xmlns="http://cisco.com/ns/yang/Cisco-IOS-XE-wireless-wlan-cfg">
        <wlan-cfg-entries>
          <wlan-cfg-entry>
            <vap-id>4</vap-id>
          </wlan-cfg-entry>
        </wlan-cfg-entries>
      </wlan-cfg-data>
    </filter>
  </get>
</rpc>
```


3. Delete WLAN

```
<rpc message-id="101" xmlns="urn:ietf:params:xml:ns:netconf:base:1.0" 
xmlns:xc="urn:ietf:params:xml:ns:netconf:base:1.0">
  <edit-config>
    <target>
      <running/>
    </target>
    <config>
      <wlan-cfg-data xmlns="http://cisco.com/ns/yang/Cisco-IOS-XE-wireless-wlan-cfg">
        <wlan-cfg-entries xc:operation="delete">
          <wlan-cfg-entry>
            <vap-id>4</vap-id>
          </wlan-cfg-entry>
        </wlan-cfg-entries>
      </wlan-cfg-data>
    </config>
  </edit-config>
</rpc>
```
