# Notes for Ayam Secure Secrets Web Source

- This repo is forked from `vaultwarden/vw_web_builds` (which is a fork of `bitwarden/clients`)
- Now vw patches are applied in this repo (`vw_web_builds`) and then referenced in `dani-garcia/bw_web_builds`
- So for AS, apply patches in this repo (`ayamsecure/secrets-web-source`) and then reference in `ayamsecure/secrets-web`

### When a new dani-garcia/bw_web_builds release has been published:

1. from terminal `git fetch upstream`
2. then checkout specific upstream release branch: https://github.com/vaultwarden/vw_web_builds/branches, `git checkout v2025.12.0`
3. checkout ayam specific branch `git checkout -b v2025.12.0-ayam`
4. apply patch: `git apply --reject --whitespace=fix ayam-secrets-web-source/ayam-v3.patch`
5. If patch fails, `find . -name "*.rej"` and resolve changes manually and create update patch file:

- try `gacm 'updating patch'` then `git format-patch -1 HEAD --stdout > path/to/my_new_custom.patch`
- OR `gacm 'updating patch'` then `git diff <commit hash from vw repo> HEAD ':(exclude)ayam-secrets-web-source' > ayam-v4.patch`

6. push changes up

## Patchfile Updates

- removed footer changes from patch, added to css template
- removed message.json updates, no longer needed
- removed app.component.html alt tag update

## Notes

```
--reject: If the patch fails for some files (because line numbers changed upstream), this option applies the parts that do work and saves the failed parts to .rej files so you can fix them manually.

--whitespace=fix: Automatically fixes common whitespace issues that might otherwise cause the patch to fail.
```
