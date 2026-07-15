# Public-repository publication checklist

Review the complete diff and generated output before publishing.

- [ ] No passwords, tokens, recovery codes, private keys, or encrypted-secret keys.
- [ ] No real public/private IP addresses, internal domains, Tailnet identifiers, or
      access-policy exports.
- [ ] No serial numbers, MAC addresses, account IDs, personal names, or email addresses.
- [ ] No camera URLs, credentials, locations, screenshots, or private scenes.
- [ ] No router/switch configuration exports or firmware backups.
- [ ] Example addresses use reserved documentation ranges and are labeled examples.
- [ ] Diagrams and screenshots contain no hidden identifiers or metadata.
- [ ] Git history contains no earlier unsanitized version of the content.
- [ ] Commands explain destructive behavior and provide validation or rollback.
- [ ] Written guidance and code declare the intended license.

Sanitization is not only redaction: examples should remain internally consistent and
usable after production-specific details are replaced.
