# Note
On April 11, 2025, the CA/Browser Forum passed a ballot to reduce the maximum validity of SSL/TLS certificates to just 47 days by 2029. 

The reduction will occur in stages to allow gradual adaptation:
March 15, 2026: Maximum validity drops to 200 days.
March 15, 2027: Further reduced to 100 days.
March 15, 2029: Final cap at 47 days

# Ansible ssl_cert_check Role

This role checks an external SSL certificate, calculates remaining validity, renews it when below threshold, and sends a notification.

## Requirements

- openssl installed on execution node
- certbot (if using certbot renewal)
- SMTP or Slack webhook for notifications

## Example Playbook

---
- hosts: localhost
  gather_facts: no
  roles:
    - role: ssl_cert_check
      vars:
        ssl_host: myapp.example.com
        renew_threshold_days: 15
        notify_method: slack
        slack_webhook_url: https://hooks.slack.com/services/XXX