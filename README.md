# FASS Cloud Native V0.1

This repository builds a **real native FASS RenderEngine** into Blender 5.2 LTS on a GitHub Windows runner.

## Important

This is **not** the old FASS Bridge. The render callback calls the FASS C++ path tracer directly and writes pixels into Blender's Render Result. There is no `FASS -> Cycles` or `FASS -> EEVEE` render path.

## V0.1 scope

V0.1 is a native-boundary test build:

- FASS is compiled into Blender.
- `Render Engine -> FASS` is native.
- F12 enters FASS C++.
- FASS calculates recursive reflection and diffuse indirect bounce itself.
- Render Result is filled by FASS.
- The validation renderer is CPU reference code and uses its own built-in test scene.

It does **not yet** translate Blender mesh/material/light data and does **not yet** use CUDA/OptiX. Those are the next milestones after the native Windows build is proven.

## Why cloud build

Your runtime PC does not need Visual Studio, CMake, Git, Blender source, CUDA SDK, or OptiX SDK. GitHub Actions builds Blender remotely; you only download the finished artifact.

## Run the cloud build

1. Put this repository on GitHub.
2. Open **Actions -> Build FASS Native Windows -> Run workflow**.
3. Leave `blender_ref = blender-v5.2-release` and choose `lite` for the first proof build.
4. Wait for the workflow to finish.
5. Download artifact `FASS-Blender-5.2-Windows-x64-lite`.
6. Extract it and run `blender.exe`.
7. In Blender choose `Render Engine -> FASS` and press F12.

A successful build runs a 96x54 background smoke render before the artifact is uploaded.

## First-run expectation

F12 renders the FASS validation scene (reflective floor, diffuse sphere, chrome sphere, emissive source). Your `.blend` scene is intentionally not consumed in V0.1. This isolates the native renderer boundary before we add Blender scene translation.

## Build profile

- `lite`: recommended for the first cloud build; smaller/faster.
- `full`: closer to a normal Blender build and requires more build time/storage.
