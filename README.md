# Flash Attention Wheels

Pre-built wheels built from [Dao-AILab/flash-attention](https://github.com/Dao-AILab/flash-attention),
for combinations upstream does not publish.

A flash-attn wheel is tied to the **exact PyTorch minor version** it was compiled against — it links
that version's libtorch C++ ABI. Installing a wheel built for a different PyTorch fails at import or
crashes inside the kernel call, so match the PyTorch column exactly.

## Available Wheels

| Version | OS | CUDA | PyTorch | Python | GPU arch | Download |
|---------|----|------|---------|--------|----------|----------|
| 2.8.3 | Linux x86_64 | 13.x | 2.14.x | 3.12 | sm_80 (Ampere, incl. RTX 30xx) | [wheel](../../releases/download/v2.8.3-linux-cu13-torch2.14/flash_attn-2.8.3%2Bcu13torch2.14-cp312-cp312-linux_x86_64.whl) |
| 2.7.4.post1 | Windows x64 | 12.8 | 2.9.x | 3.11 | default set | [wheel](../../releases/download/v2.7.4.post1/flash_attn-2.7.4.post1%2Bcu128torch2.9-cp311-cp311-win_amd64.whl) |

## Install

Linux / CUDA 13 / PyTorch 2.14 / Python 3.12:

```bash
pip install https://github.com/zdaar/flash-attention-wheels/releases/download/v2.8.3-linux-cu13-torch2.14/flash_attn-2.8.3%2Bcu13torch2.14-cp312-cp312-linux_x86_64.whl
```

Windows / CUDA 12.8 / PyTorch 2.9 / Python 3.11:

```bash
pip install https://github.com/zdaar/flash-attention-wheels/releases/download/v2.7.4.post1/flash_attn-2.7.4.post1%2Bcu128torch2.9-cp311-cp311-win_amd64.whl
```

## Build Info

**2.8.3 — Linux**

- OS: Arch Linux
- CUDA Toolkit: 13.3, host compiler g++-15
- `FLASH_ATTN_CUDA_ARCHS=80` only. sm_80 code runs on sm_86 consumer Ampere; **not** built for
  Hopper (sm_90) or Blackwell (sm_100/sm_120).
- Needs `sed -i 's/-std=c++17/-std=c++20/g' setup.py` first: flash-attn 2.8.3 hardcodes C++17 on the
  CUDA path, while PyTorch >= 2.14 headers require C++20. Without it the build fails with ~1100
  errors inside PyTorch's own headers.

**2.7.4.post1 — Windows**

- OS: Windows 11
- Compiler: MSVC 14.44 (VS2022)
- CUDA Toolkit: 12.8.61
