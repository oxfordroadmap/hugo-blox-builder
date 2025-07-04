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
# **commit hash** and **commit timestamp** 

using standard Windows Command Prompt

### 🧩 1. **Get the full commit hash**

Open **Command Prompt** in your repository folder and run:

cmd

```
git log -1 --pretty=format:"%H"
```

This will return something like:

```
8b683644319a931af94fb5d8b65f637ced7fd4c4
```

✅ You **must use the full hash** (all 40 characters) in your pseudo-version tag—short hashes (like the first 7 chars) work for browsing, but not for `go.mod`.

### 🕒 2. **Get the UTC timestamp in Go format**

Still in Command Prompt, run this two-step process:

#### Step 1: Get the Unix timestamp

cmd

```
git log -1 --pretty=format:"%ct"
```

Example output:

```
1751631956
```

#### Step 2: Convert to UTC timestamp (`YYYYMMDDHHMMSS`)

You’ll need to use an external method because Windows Command Prompt doesn’t support direct timestamp formatting. Here are two options:

#### 👉 Option A: Use https://www.unixtimestamp.com

Paste `1751625724` into the field and get the UTC date formatted as:

```
20250704122556
```

#### 👉 Option B: Use PowerShell just for conversion (optional fallback):

powershell

```
(Get-Date "1970-01-01 00:00:00Z").AddSeconds(1751631956).ToUniversalTime().ToString("yyyyMMddHHmmss")
```

### 🏷️ Your final pseudo-version tag would look like:

```
v0.0.2-20250704122556-8b683644319a931af94fb5d8b65f637ced7fd4c4
```

Now place this inside your `go.mod` like:

go

```
replace github.com/HugoBlox/hugo-blox-builder => github.com/oxfordroadmap/hugo-blox-builder v0.0.2-20250704122556-8b683644319a931af94fb5d8b65f637ced7fd4c4
```

And you're good to run:

cmd

```
hugo mod tidy
```



