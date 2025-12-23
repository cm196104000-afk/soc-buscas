# soc-buscas
Busca de Socs Cargo Blue
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <title>Busca de SOCs</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    body { font-family: Arial, sans-serif; background: #f3f4f6; padding: 20px; }
    input { width: 100%; padding: 12px; margin-bottom: 20px; }
    .card { background: #fff; padding: 15px; margin-bottom: 12px; border-radius: 6px; }
  </style>
</head>
<body>

  <h2>Pesquisa de SOCs e Rotas</h2>
  <input id="busca" placeholder="Digite cidade, SOC, HUB ou endereço" />

  <div id="resultados"></div>

  <script>
    fetch("rotas.json")
      .then(res => res.json())
      .then(dados => {
        const input = document.getElementById("busca");
        const resultados = document.getElementById("resultados");

        input.addEventListener("input", () => {
          const termo = input.value.toLowerCase();
          resultados.innerHTML = "";

          dados
            .filter(item => {
              const texto = Object.values(item).join(" ").toLowerCase();
              return texto.includes(termo);
            })
            .forEach(item => {
              resultados.innerHTML += `
                <div class="card">
                  <strong>Origem:</strong> ${item.Origem}<br>
                  <strong>Endereço Origem:</strong> ${item.Endereco_Origem}<br>
                  <strong>Destino:</strong> ${item.Destino}<br>
                  <strong>Endereço Destino:</strong> ${item.Endereco_Destino}<br>
                  <strong>KM:</strong> ${item.KM}<br>
                  <strong>Tempo:</strong> ${item.Tempo}
                </div>
              `;
            });
        });
      });
  </script>

</body>
</html>

