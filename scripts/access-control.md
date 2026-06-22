# UniFi Access & Network Scripts

Command snippets for UniFi Access door/gate control and a few Dream Machine network tasks, pulled from real installs. Every IP, token, and door ID is a placeholder — fill in your own.

For the full collection (cameras, doorbell integration, more scripts), see [homelab-runbook](https://github.com/Sparky-Venture-Labs/homelab-runbook).

---

## List UniFi Access Doors

```bash
curl -k -X GET "https://<UNIFI_GATEWAY_IP>:12445/api/v1/developer/doors" \
  -H "Authorization: Bearer <API_TOKEN>" \
  -H "accept: application/json" \
  -H "content-type: application/json"
```

---

## List UniFi Access Doors (Get Door IDs)

```bash
curl -k -X GET "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json"
```

---

## Unlock Main Gate (UniFi Access)

```bash
UNIFI_HOST="https://<UNIFI_GATEWAY_IP>:12445"
DOOR_ID="<MAIN_GATE_DOOR_ID>"
API_TOKEN="<API_TOKEN>"

curl -k -sS -X PUT "${UNIFI_HOST}/api/v1/developer/doors/${DOOR_ID}/unlock" \
  -H "Authorization: Bearer ${API_TOKEN}" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"actor_name":"Savant Main Gate"}'
```

---

## Unlock Main Gate (UniFi Access API)

```bash
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/unlock" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"actor_name": "Savant Main Gate"}'
```

---

## Unlock Service Gate (UniFi Access)

```bash
UNIFI_HOST="https://<UNIFI_GATEWAY_IP>:12445"
DOOR_ID="<SERVICE_GATE_DOOR_ID>"
API_TOKEN="<API_TOKEN>"

curl -k -sS -X PUT "${UNIFI_HOST}/api/v1/developer/doors/${DOOR_ID}/unlock" \
  -H "Authorization: Bearer ${API_TOKEN}" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"actor_name":"Savant Service Gate"}'
```

---

## Unlock Service Gate (UniFi Access API)

```bash
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/unlock" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"actor_name": "Savant Service Gate"}'
```

---

## Hold Gate Open (lock_rule: keep_unlock)

```bash
# Hold Main Gate open indefinitely:
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/lock_rule" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"type":"keep_unlock"}'

# Hold Service Gate open indefinitely:
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/lock_rule" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"type":"keep_unlock"}'
```

---

## Release Gate (Reset to Normal Schedule)

```bash
# Reset Main Gate to normal schedule:
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/lock_rule" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"type":"reset"}'

# Reset Service Gate to normal schedule:
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/lock_rule" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"type":"reset"}'
```

---

## UniFi Access API – Lock Door

```bash
curl -k -sS -X PUT "https://<UNIFI_GATEWAY_IP>:12445/api/v1/developer/doors/<DOOR_ID>/lock" \
  -H "Authorization: Bearer <API_TOKEN>" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"actor_name":"Manual Lock"}'
```

---

## UniFi — Lock Door via API

```bash
# Force-lock Main Gate (keep_lock):
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/lock_rule" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"type":"keep_lock"}'

# Force-lock Service Gate:
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/lock_rule" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"type":"keep_lock"}'

# Timed unlock (15 minutes then auto-lock):
curl -k -sS -X PUT "https://<SAVANT_HOST_IP>:12445/api/v1/developer/doors/<DOOR_ID>/lock_rule" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{"type":"custom","interval":15}'
```

---

## UniFi Access API — Webhook Registration (Doorbell)

```bash
# Register webhook for doorbell/intercom press events:
curl -k -sS -X POST "https://<SAVANT_HOST_IP>:12445/api/v1/developer/webhooks" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN" \
  -H "accept: application/json" \
  -H "content-type: application/json" \
  -d '{
    "url": "http://<LOCAL_IP>:8084/doorbell-press",
    "events": ["access.doorbell.incoming"]
  }'

# List existing webhooks:
curl -k -sS -X GET "https://<SAVANT_HOST_IP>:12445/api/v1/developer/webhooks" \
  -H "Authorization: Bearer YOUR_UNIFI_API_TOKEN"
```

---

## Gate Status Script (Poll UniFi Lock State)

```bash
# /Users/Shared/unifi-gate-status.sh
#!/bin/bash

UNIFI_HOST="https://<SAVANT_HOST_IP>:12445"
API_TOKEN="YOUR_UNIFI_API_TOKEN"
MAIN_ID="<DOOR_ID>"
SERVICE_ID="<DOOR_ID>"

function door_status() {
  local name="$1"
  local id="$2"
  json=$(curl -k -sS -X GET "${UNIFI_HOST}/api/v1/developer/doors/${id}" \
    -H "Authorization: Bearer ${API_TOKEN}" \
    -H "accept: application/json" \
    -H "content-type: application/json")
  lock_state=$(echo "$json" | python3 -c "import sys, json; d=json.load(sys.stdin); print(d['data']['door_lock_relay_status'])")
  pos_state=$(echo "$json" | python3 -c "import sys, json; d=json.load(sys.stdin); print(d['data']['door_position_status'])")
  echo "${name}:${lock_state}:${pos_state}"
}

door_status "MAIN_GATE" "$MAIN_ID"
door_status "SERVICE_GATE" "$SERVICE_ID"
```

---

## UniFi Network API — Dump Config (from UDM SSH)

```bash
# From inside UDM SSH session:
# Step 1 — Login and get cookie:
curl -sk -X POST https://localhost/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"YOUR_UI_PASSWORD"}' \
  -c /tmp/cookies.txt

# Step 2 — Dump network config:
curl -sk https://localhost/proxy/network/api/s/default/rest/networkconf \
  -b /tmp/cookies.txt

# Alternative: Use API key (newer UniFi OS 4.x+):
curl -k -X GET 'https://<UNIFI_GATEWAY_IP>/proxy/network/integration/v1/sites' \
  -H 'X-API-KEY: <API_TOKEN>'
```

---

## UniFi — Check Interface Stats from SSH

```bash
# Check interface config:
ifconfig | grep 'inet '

# Check active connections:
netstat -an | grep ESTABLISHED

# Check listening ports:
netstat -an | grep LISTEN

# Check routing table:
netstat -rn
```

---

## UniFi — MAC Filtering on Switch Ports

```bash
# Via UniFi GUI:
# Devices → Select Switch → Port Manager → Click Port → Mode: Restricted by MAC ID → Add MACs

# Via 802.1X RADIUS MAC Auth (covers UDM built-in ports too):
# Settings → System → RADIUS → Enable Default RADIUS Server
# Add device: username=aabbccddeeff, password=aabbccddeeff (MAC no separators)
# Settings → Networks → Global Switch Settings → Enable 802.1X Control
```

---

## UniFi — WPA3 Enable + RADIUS MAC Auth

```bash
# Enable WPA3 on SSID:
# Settings → WiFi → Select SSID → Security → WPA3 (or WPA2/3 mixed)

# Enable RADIUS MAC Auth on WiFi:
# Settings → WiFi → Select SSID → Advanced → RADIUS MAC Authentication → Enable
# Point to Default RADIUS Server

# Verify RADIUS is running (from UDM SSH):
netstat -an | grep 7812
# RADIUS listens on port 7812/7813 (PPSK ports)
```

