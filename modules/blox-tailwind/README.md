# Hugo Blox Tailwind UI

The Hugo Blox web framework utilising [TailwindCSS](https://tailwindcss.com/) and its [typography plugin](https://tailwindcss.com/docs/typography-plugin) for styling components.

See the Blog Starter Template for an example using this module.

## Development

```bash
hugo mod npm pack
npm install
```

You need to add this to your `config.yaml` to enable Hugo's Tailwind integration:

```yaml
build:
  writeStats: true
```


## Upgrading 
* from : tailwindcss@3.3.5
* to :  tailwindcss@3.4.17

---

To generate a clean, minimal `pnpm-lock.yaml` that aligns exactly with your existing environment files—without bringing in stale or overlapping versions—here’s your structured path forward 🧭

---

### ✅ Goal
You want `pnpm-lock.yaml` to:
- Reflect only what’s declared in your `package.json`
- Respect the dynamic Tailwind/PostCSS config
- Avoid legacy or duplicated dependency versions

---

### 🛠️ Step-by-step

#### 🔹 1. **Ensure working directory is clean**
Navigate to the module directory:
```bash
cd modules/blox-tailwind
```

Optional cleanup:
```bash
rm -rf node_modules pnpm-lock.yaml
pnpm store prune
```

This removes symlinks and cached store references that could pollute resolution.

---

#### 🔹 2. **Run install using lockfile-only flag**
Now generate your lockfile:
```bash
pnpm install --lockfile-only
```

> This **does not install** packages physically—it only resolves dependency versions and writes the lockfile.

You’ll get a `pnpm-lock.yaml` scoped precisely to your `package.json` setup and environmental plugins like `tailwindcss`, `autoprefixer`, and `postcss-import`.

---

#### 🔹 3. **Verify lockfile clarity**
Use these commands to audit the result:
```bash
pnpm list --depth=Infinity
pnpm why tailwindcss
```

These help confirm that dependencies match expectations—no excess layers or peer version conflicts.

---

### 💡 Optional Enhancements

- **Ensure reproducibility in CI**:
  ```bash
  pnpm install --frozen-lockfile
  ```
  That guarantees `pnpm-lock.yaml` won’t be modified during install.

- **Prevent hoisting quirks**:
  In `.npmrc` (optional):
  ```
  shamefully-hoist=false
  auto-install-peers=false
  ```

---

Would you like help scripting this for Hugo modules or packaging it into a reusable starter template? You’ve got a sophisticated setup—let’s make it frictionless across environments.