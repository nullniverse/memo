---
title: python-gnupg
date: 20221129
author: Lyz
---

[python-gnupg](https://github.com/vsajip/python-gnupg) is a Python library to
interact with `gpg` taking care of the internal details and allows its users to
generate and manage keys, encrypt and decrypt data, and sign and verify
messages.

# [Installation](https://github.com/vsajip/python-gnupg#installing-from-pypi)

```bash
pip install python-gnupg
```

# [Usage](https://gnupg.readthedocs.io/en/latest/#getting-started)

You interface to the GnuPG functionality through an instance of the GPG class:

```python
gpg = gnupg.GPG(gnupghome="/path/to/home/directory")
```

Note: I've already created an adapter for gpg called `KeyStore` available in [`pass-collaborate`](https://github.com/lyz-code/pass-collaborate)

- Decrypt a file:

  ```python
  gpg.decrypt_file("path/to/file")
  ```

  Note: You can't pass `Path` arguments to `decrypt_file`.

- [Encrypt a file](https://gnupg.readthedocs.io/en/latest/#encryption):

  ```python
  gpg.encrypt_file('path/to/file', recipients)
  ```

  Where `recipients` is a `List[str]` of gpg Key IDs.

- [List private keys](https://gnupg.readthedocs.io/en/latest/index.html?highlight=list%20private#listing-keys):

  ```python
  >>> public_keys = gpg.list_keys()
  >>> private_keys = gpg.list_keys(True)
  ```

- [List the recipients that can decrypt a file](https://docs.red-dove.com/python-gnupg/#finding-the-recipients-for-an-encrypted-message)
  
  ```python
  def list_recipients(self, path: Path) -> List['GPGKey']:
      """List the keys that can decrypt a file.

      Args:
          path: Path to the file to check.
      """
      keys = []
      for short_key in self.gpg.get_recipients_file(str(path)):
          keys.append(self.gpg.list_keys(keys=[short_key])[0]['fingerprint'])

      return keys
  ```

- [Get information of a key](
# References

- [Docs](https://gnupg.readthedocs.io/en/latest/)
- [Source](https://github.com/vsajip/python-gnupg)
- [Issues](https://github.com/vsajip/python-gnupg/issues)
