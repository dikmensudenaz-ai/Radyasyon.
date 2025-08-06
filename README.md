# Radyasyon.
Radyasyonvedsup
import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

st.title("🌌 DSUP ve Melanin Üretimi Simülasyonu")
st.subheader("Radyasyon Dozuna Karşı Gen İfadesi Modeli")

def hill_function(dose, k, n):
    return (dose ** n) / (k ** n + dose ** n)

dose = st.slider("Radyasyon Dozu (Gy)", min_value=0.0, max_value=50.0, value=10.0, step=0.5)

k_dsup = 12
n_dsup = 3
k_melanin = 8
n_melanin = 2

dsup_output = hill_function(dose, k_dsup, n_dsup)
melanin_output = hill_function(dose, k_melanin, n_melanin)

st.write(f"🧬 **DSUP Üretimi:** {dsup_output * 100:.2f}%")
st.write(f"🎨 **Melanin Üretimi:** {melanin_output * 100:.2f}%")

dose_range = np.linspace(0, 50, 500)
dsup_curve = hill_function(dose_range, k_dsup, n_dsup)
melanin_curve = hill_function(dose_range, k_melanin, n_melanin)

fig, ax = plt.subplots()
ax.plot(dose_range, dsup_curve, label="DSUP", linewidth=2)
ax.plot(dose_range, melanin_curve, label="Melanin", linestyle='--', linewidth=2)
ax.axvline(dose, color='red', linestyle=':', label=f"Doz: {dose} Gy")
ax.set_xlabel("Radyasyon Dozu (Gy)")
ax.set_ylabel("Gen İfadesi (0 - 1)")
ax.set_title("Gen İfadesi Eğrisi")
ax.legend()
ax.grid(True)

st.pyplot(fig)
