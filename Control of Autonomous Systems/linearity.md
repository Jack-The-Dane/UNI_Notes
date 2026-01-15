# Linear vs Non-linear Systems of Coupled Differential Equations

A **system of coupled differential equations** is classified as **linear** or **non-linear** based on how the unknown functions and their derivatives appear in the equations—not on how many equations there are or how they are coupled.

---

## 1. Linear Systems of Differential Equations

A system is **linear** if **each equation is linear in the unknown functions and their derivatives**.

### Formal definition

A system for unknown functions \(x_1(t), x_2(t), \dots, x_n(t)\) is linear if it can be written in the form

\[
\sum_{j=1}^n a_{ij}(t)\,x_j'(t)
\;+\;
\sum_{j=1}^n b_{ij}(t)\,x_j(t)
\;=\;
f_i(t),
\quad i = 1,\dots,n
\]

where:
- \(a_{ij}(t)\), \(b_{ij}(t)\), and \(f_i(t)\) depend **only on the independent variable** (e.g. time \(t\)),
- the unknown functions \(x_j\) and their derivatives appear **only to the first power**,
- there are **no products**, powers, or nonlinear functions of the unknowns.

Coupling is allowed, as long as it is linear.

---

### What is allowed in linear systems

- Linear combinations of variables  
- Linear combinations of derivatives  
- Time-dependent coefficients  
- Multiple equations influencing each other  

---

### What is *not* allowed

- Products like \(x_1 x_2\)  
- Powers like \(x^2\), \((x')^2\)  
- Nonlinear functions like \(\sin(x)\), \(e^x\)  
- Coefficients that depend on the unknowns  

---

### Example 1: Linear coupled system

\[
\begin{aligned}
\frac{dx}{dt} &= 3x + 2y \\
\frac{dy}{dt} &= -x + 4y
\end{aligned}
\]

This system is **linear**:
- \(x\) and \(y\) appear only to the first power,
- the coupling (\(2y\), \(-x\)) is linear.

Matrix form:
\[
\frac{d}{dt}
\begin{pmatrix} x \\ y \end{pmatrix}
=
\begin{pmatrix}
3 & 2 \\
-1 & 4
\end{pmatrix}
\begin{pmatrix} x \\ y \end{pmatrix}
\]

---

### Example 2: Linear but non-homogeneous system

\[
\begin{aligned}
\frac{dx}{dt} &= x + y + \sin t \\
\frac{dy}{dt} &= 2x - y + t^2
\end{aligned}
\]

This system is still **linear**, because \(\sin t\) and \(t^2\) depend only on \(t\), not on the unknowns.

---

## 2. Non-linear Systems of Differential Equations

A system is **non-linear** if **any equation contains a nonlinear dependence on the unknown functions or their derivatives**.

Even a *single* nonlinear term makes the entire system non-linear.

---

### Common sources of nonlinearity

- Products of unknowns: \(xy\)
- Powers of unknowns: \(x^2\), \(y^3\)
- Nonlinear functions of unknowns: \(\sin(x)\), \(e^y\)
- Products involving derivatives: \(x\,x'\), \((y')^2\)

---

### Example 3: Non-linear due to products

\[
\begin{aligned}
\frac{dx}{dt} &= x y \\
\frac{dy}{dt} &= x - y
\end{aligned}
\]

The term \(xy\) makes the system **non-linear**.

---

### Example 4: Non-linear due to powers

\[
\begin{aligned}
\frac{dx}{dt} &= x^2 + y \\
\frac{dy}{dt} &= y
\end{aligned}
\]

The \(x^2\) term makes the system **non-linear**, even though the second equation is linear.

---

### Example 5: Non-linear due to nonlinear functions

\[
\begin{aligned}
\frac{dx}{dt} &= \sin(x) + y \\
\frac{dy}{dt} &= x
\end{aligned}
\]

The \(\sin(x)\) term introduces non-linearity.

---

## 3. Key Conceptual Takeaway

**Linearity concerns the dependence on the unknowns, not on coupling or complexity.**

- A system can be **highly coupled and still linear**
- A system with just one nonlinear term is **non-linear**
- Linear systems obey the **superposition principle**
- Non-linear systems do **not**

---

## 4. Summary Table

| Feature | Linear system | Non-linear system |
|------|--------------|------------------|
| Unknowns appear to power > 1 | ❌ | ✅ |
| Products of unknowns | ❌ | ✅ |
| Nonlinear functions of unknowns | ❌ | ✅ |
| Time-dependent coefficients | ✅ | ✅ |
| Superposition principle | ✅ | ❌ |

---

If you’d like, I can also explain:
- linearization of nonlinear systems,
- physical examples (springs, circuits),
- or solution methods for linear systems.
