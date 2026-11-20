# [Nuclear Shell Model: Bound States and Shell Structure](https://obayrak.github.io/ShellModel/)

**▶ Live app: [obayrak.github.io/ShellModel](https://obayrak.github.io/ShellModel/)**

An interactive browser simulator that solves the radial Schrödinger equation for 17 nuclear and atomic potentials. It shows bound-state energies and wavefunctions, compares them with WKB and exact results, and builds the nuclear shell model with its magic numbers.

Everything is in a single `index.html` file. There is no backend, no build step and no install.

---

## Features

The app has two modes, selected with the tabs at the top.

### 1. Bound states

- **Potential library** with 17 potentials, which you can tick and add together:
  - *Well and barrier:* infinite square well, finite well with barrier
  - *Coulomb family:* point Coulomb, Yukawa, Debye-screened Coulomb, screened Coulomb with cosine (Friedel) oscillations
  - *Oscillator and molecular:* harmonic oscillator with any power n, Kratzer, Morse
  - *Exactly solvable:* Hulthén, Pöschl–Teller, Rosen–Morse II, cosh
  - *Nuclear:* Woods–Saxon volume, Woods–Saxon surface (derivative), Woods–Saxon with Coulomb, Woods–Saxon spin–orbit
- **Two-body system:** pick two particles (nucleon, p, n, e⁻, μ⁻, π⁻, d, t, ³He, α, ¹²C, ¹⁶O, ⁴⁰Ca, ²⁰⁸Pb, a fixed centre, or custom masses and charges). The app uses the reduced mass μ = m₁m₂/(m₁+m₂) and can add the Coulomb potential Z₁Z₂e²/r with a finite charge radius.
- **Angular momentum:** set ℓ (s, p, d, …) and choose j = ℓ ± ½ for the spin–orbit term.
- **Plot:** shows the effective potential, the energy levels, u(r) or |u(r)|², the classically forbidden regions and the turning points. Units switch automatically from MeV and fm to keV or eV and pm or Å.
- **Bound-state table:** lists each state's energy, the exact analytic value where one exists, the WKB estimate and its error, ⟨r⟩, r_rms, the probability of being in the forbidden region, and the number of nodes.
- **20 ready-made example models** in four groups: benchmarks with exact answers, nuclear physics (the deuteron, ⁴⁰Ca and ²⁰⁸Pb), two-body systems (hydrogen, muonic hydrogen, muonic lead, p + ⁴⁰Ca, α + ¹⁶O), and screened or molecular wells.

### 2. Nuclear shell model

- A Woods–Saxon potential with spin–orbit coupling and Coulomb for protons. The depth comes from the Bohr–Mottelson formula V₀ = 51 ∓ 33(N−Z)/A MeV, or you can set it by hand.
- **Single-particle level diagram** that shows occupied, partly filled and empty levels, and detects shell gaps automatically.
- **Magic numbers:** gaps are compared with the known values 2, 8, 20, 28, 50, 82, 126 and 184. Set the spin–orbit strength κ to 0 to see why spin–orbit coupling is needed for 28 and above.
- **Ground-state Jπ prediction** from the extreme single-particle model. Odd–odd nuclei use Nordheim's rules. Each prediction is checked against the measured value.
- More than 30 example nuclei: doubly magic nuclei, one nucleon or one hole outside a closed shell, odd-A, odd–odd and open-shell nuclei. You can also enter a custom A and Z.
- The radial wavefunction and a level table with E, 2j+1, the running total, ⟨r⟩, r_rms and occupation.
- **Measured data for every known nucleus** from NUBASE2020 (3,558 ground states, embedded in the page):
  - the measured Jπ, labelled *measured*, *tentative* or *systematics estimate*, compared with the model's prediction for any A and Z
  - the half-life or stability
  - one- and two-nucleon separation energies (Sₙ, Sₚ, S₂ₙ/2, S₂ₚ/2) computed from the mass excesses, compared with the model's last filled level, and shown as a line on the level diagram
- **Levels against a parameter:** plots every single-particle energy while sweeping N (isotopes), Z (isotones), A (along the valley of stability), κ, V₀, r₀ or a. The model Fermi level is drawn as a thick line, and measured −S and −S₂/2 from NUBASE2020 are overlaid. Click the plot to jump to that value.

### General

- Night and day themes
- Interactive Plotly charts with zoom, hover and PNG export
- Works on desktop and mobile

---

## Numerical method

The substitution ψ = u(r)/r · Y_ℓm turns the 3D problem into the radial equation

```
−(ℏ²/2μ) u″(r) + [V(r) + ℏ²ℓ(ℓ+1)/(2μr²)] u(r) = E u(r),   u(0) = u(r_max) = 0
```

- The second derivative is replaced by finite differences, which gives a symmetric tridiagonal matrix.
- Eigenvalues are found with **Sturm-sequence bisection** and eigenvectors with **inverse iteration**. Each u is normalised so that ∫u² dr = 1.
- The **WKB** estimate uses the Langer correction ℓ(ℓ+1) → (ℓ+½)², which makes it exact for the harmonic oscillator and Coulomb potentials.

Units are MeV and fm, with ℏc = 197.327 MeV·fm and e²/4πε₀ = 1.44 MeV·fm.

---

## Limitations

- The shell model is the extreme single-particle picture. It ignores the residual interaction, configuration mixing and deformation, so predictions for deformed nuclei (for example A ≈ 150–190 or A ≥ 222) are only a rough guide.
- States whose wavefunction reaches the box edge are marked ⚠. Increase r_max for accurate energies.
- Positive-energy states held in by a barrier are quasi-bound, marked ≈. Their energies depend on the box size.

---

## Data

Measured ground-state data comes from **NUBASE2020**: F. G. Kondev, M. Wang, W. J. Huang, S. Naimi and G. Audi, *Chinese Physics C* **45**, 030001 (2021), doi:[10.1088/1674-1137/abddae](https://doi.org/10.1088/1674-1137/abddae). NUBASE2020 does not contain charge radii.

## Related project

- [NUBASE2020 · Decay Systematics Explorer](https://obayrak.github.io/NUBASE/)

---

## License

This project is licensed under the **GNU General Public License v3.0**. See [`LICENSE`](LICENSE) for the full text.
