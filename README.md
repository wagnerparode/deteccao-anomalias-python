# ==========================================================
# PROJETO: DETECTOR DE TRANSAÇÕES SUSPEITAS (VERSÃO INICIANTE)
# ==========================================================

transacoes = [
    {"id": 1, "valor": 50.00,  "hora": 14},
    {"id": 2, "valor": 120.00, "hora": 20},
    {"id": 3, "valor": 4500.00, "hora": 3},  # Alerta
    {"id": 4, "valor": 15.00,  "hora": 10},
    {"id": 5, "valor": 3200.00, "hora": 15}, # Alerta
    {"id": 6, "valor": 80.00,  "hora": 2},   # Alerta
]

print("--- INICIANDO ANÁLISE DE TRANSAÇÕES --- \n")

total_analisado = 0
total_alertas = 0

for t in transacoes:
    total_analisado += 1
    valor_limite = 2000.00
    madrugada_inicio = 0
    madrugada_fim = 5
    
    se_valor_alto = t["valor"] > valor_limite
    se_madrugada = t["hora"] >= madrugada_inicio and t["hora"] <= madrugada_fim
    
    if se_valor_alto or se_madrugada:
        total_alertas += 1
        print(f"🚨 ALERTA NA TRANSAÇÃO {t['id']}:")
        print(f"   -> Valor: R$ {t['valor']:.2f}")
        print(f"   -> Horário: {t['hora']}h")
        
        if se_valor_alto and se_madrugada:
            print("   -> Motivo: Valor crítico e horário perigoso!")
        elif se_valor_alto:
            print("   -> Motivo: Valor acima do limite permitido.")
        else:
            print("   -> Motivo: Horário de madrugada suspeito.")
        print("-" * 40)

print("\n=== RESUMO DA ANÁLISE ===")
print(f"Total de transações verificadas: {total_analisado}")
print(f"Total de alertas de anomalia gerados: {total_alertas}")
