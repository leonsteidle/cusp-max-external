# cusp~ : Cusp Catastrophe External for Max/MSP

**Author:** Leon Steidle  
**Version:** 2025  
**License:** © 2025 Leon Steidle. All rights reserved.

## Overview

`cusp~` is a Max/MSP external that calculates the real roots of the cubic equation associated with René Thom's cusp catastrophe potential.  
It outputs:

1. Lower stable root (`z0`)
2. Unstable root (`z1`)
3. Upper stable root (`z2`)
4. Current branch/state (`0 = lower`, `1 = upper`)
5. Discriminant (`D`) of the cubic — indicates whether the system is inside (`D < 0`) or outside (`D > 0`) the bifurcation set.

**Inputs (audio signals, left → right):**
- `alpha` — controls the constant term of the cubic
- `beta` — controls the quadratic term (scaled by width)
- `width` — global scaling of beta (kept for backward compatibility)

**Outputs (audio signals, left → right):**
- `z0` — lower stable root  
- `z1` — unstable root  
- `z2` — upper stable root  
- `state` — branch: 0 = lower, 1 = upper  
- `D` — discriminant of the cubic

---

## Requirements

- **Max/MSP SDK**: Download from [Cycling '74](https://cycling74.com/sdk)
  - Make sure the [max-sdk-base](https://github.com/Cycling74/max-sdk-base) submodules are present and paths are set in the Makefile.

- **C Compiler:**  
  - macOS: `clang` (default on macOS)
  - Linux: *not supported for Max/MSP externals*
  - Windows: Not directly supported by this Makefile.

- **GNU Scientific Library (GSL):**
  - *Not required for this object!*  
    All cubic root calculations are handled internally and do **not** rely on GSL or other external math libraries.
  - **If you intend to use GSL for other code, install via:**  
  - Install via:**  
    - macOS: `brew install gsl`
    - Ubuntu: `sudo apt-get install libgsl-dev`

---

## Building

1. **Clone or copy the source code** into a folder.
2. **Adjust the `MAXSDK` path** in the `Makefile` to point to your local Max SDK root if needed (default: `../../max-sdk-base`).
3. **Open a terminal** in the folder and run:

   ```sh
   make
   ```

   This will create a universal binary bundle named `cusp~.mxo` in the folder.

4. **Copy `cusp~.mxo`** to your Max/MSP externals folder or any folder in Max's search path.

---

## Usage

- In Max/MSP, create an object box and type `cusp~`
- Connect three audio signals to its three inlets (alpha, beta, width)
- The object outputs the roots and discriminant as described above

---

## Troubleshooting

- **"max-sdk-base" not found:**  
  Edit the `MAXSDK` variable in the `Makefile` to point to your Max SDK location.
- **Build errors about missing headers:**  
  Ensure the SDK paths are set correctly and you are using a compatible compiler (typically `clang` on macOS).
- **GSL errors:**  
  This object does NOT require GSL. If you see GSL errors, check that you are not including unnecessary libraries or code.

---

## Credits

- **Author:** Leon Steidle  
- **Special thanks:** Inspired by catastrophe theory and Max/MSP DSP external conventions

---

## License

© 2025 Leon Steidle. All rights reserved.
