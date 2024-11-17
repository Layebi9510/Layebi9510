import streamlit as st

# Variables globales
mot_de_passe_secret = "python123"
essais_restants = 3
points = 100

# Interface graphique avec Streamlit
st.title("💻 Jeu de Mot de Passe")
st.write("Entrez le mot de passe pour désactiver le laser !")

# Zone de saisie pour le mot de passe
mot_de_passe_saisi = st.text_input("Mot de passe", type="password")

# Fonction pour vérifier le mot de passe
if st.button("Vérifier"):

    global essais_restants, points

    if mot_de_passe_saisi == mot_de_passe_secret:
        st.success(f"✅ Laser désactivé ! Vous avez réussi avec {points} points.")
    elif mot_de_passe_saisi == "admin":
        st.success("🔓 Accès administrateur activé. Tous les systèmes sont désactivés.")
    else:
        essais_restants -= 1
        points -= 25
        if essais_restants > 0:
            if essais_restants == 2:
                st.info("💡 Indice : Le mot de passe commence par 'p'.")
            elif essais_restants == 1:
                st.info("💡 Indice : C’est un mot souvent associé à la programmation.")
            st.error(f"❌ Mauvais mot de passe. Il vous reste {essais_restants} essais.")
        else:
            st.error("⏳ Plus d'essais. Le laser s'active... GAME OVER.")
