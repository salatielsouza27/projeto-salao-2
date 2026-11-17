import streamlit as st
import sqlite3
from database import init_db, salvar_agendamento, listar_agendamentos

st.title("Agendamento de Salão")
init_db()

with st.form("agendamento"):
    nome=st.text_input("Nome")
    data=st.date_input("Data")
    horario=st.text_input("Horário")
    enviar=st.form_submit_button("Agendar")

if enviar:
    salvar_agendamento(nome,str(data),horario)
    st.success("Agendamento realizado!")

st.subheader("Agendamentos")
st.dataframe(listar_agendamentos())
