import sqlite3
import pandas as pd

def conectar():
    return sqlite3.connect("agendamentos.db",check_same_thread=False)

def init_db():
    conn=conectar()
    conn.execute("CREATE TABLE IF NOT EXISTS agendamentos(id INTEGER PRIMARY KEY,nome TEXT,data TEXT,horario TEXT)")
    conn.commit(); conn.close()

def salvar_agendamento(nome,data,horario):
    conn=conectar()
    conn.execute("INSERT INTO agendamentos(nome,data,horario) VALUES(?,?,?)",(nome,data,horario))
    conn.commit(); conn.close()

def listar_agendamentos():
    conn=conectar()
    df=pd.read_sql_query("SELECT * FROM agendamentos",conn)
    conn.close()
    return df
