from flask import Flask, request, redirect, render_template

app = Flask(__name__)


@app.route("/cadastro", methods=["POST", "GET"])
def cadastro():
    if request.method == "POST":
        matricula = request.form["matricula"]
        email = request.form["email"]
        senha = request.form["senha"]

    # Simulação de armazenamento (futuro: banco de dados)
    with open("usuarios.txt", "a") as file:
        file.write(f"{matricula},{email},{senha}\n")

    return redirect("/confirmacao")
    return render_template("Cadastro.html")  # Ou outro template com o formulário

@app.route("/comentario", methods=["POST", "GET"])
def comentario():
    materia = request.form["materia"]
    comentario = request.form["comentario"]

    # Simulação de armazenamento (futuro: banco de dados)
    with open("comentarios.txt", "a") as file:
        file.write(f"{materia}: {comentario}\n")

    return redirect("/atividades_aluno")

@app.route("/cadastro_professor", methods=["POST", "GET"])
def cadastro_professor():
    nome = request.form["nome"]
    usuario = request.form["usuario"]
    email = request.form["email"]
    senha = request.form["senha"]

    # Simulação de armazenamento (futuro: banco de dados)
    with open("professores.txt", "a") as file:
        file.write(f"{nome},{usuario},{email},{senha}\n")

    return redirect("/confirmacao_professor")

@app.route("/login", methods=["POST"])
def login():
    matricula = request.form["matricula"]
    senha = request.form["senha"]

    if matricula == "123456" and senha == "senha123":  # Apenas um exemplo simples
        return redirect("/dashboard")
    else:
        return "Credenciais inválidas!"

@app.route("/login_professor", methods=["POST" , "GET"])
def login_professor():
    if request.method == "POST":
        usuario = request.form["usuario"]
        senha = request.form["senha"]

    if usuario == "professor123" and senha == "senha_professor":  # Simulação
        return redirect("/dashboard_professor")
    else:
        return "Credenciais inválidas!"

    return render_template("login_professor.html")  # exemplo de formulário

@app.route("/dashboard_aluno")
def dashboard_aluno():
    saldo_scoins = 100  # Exemplo: saldo inicial
    desafios = ["Entregar trabalho antecipado (+20 SCoins)",
                "Participação em aula (+10 SCoins)", "Ajudar um colega (+15 SCoins)"]
    recompensas = ["Caneta personalizada - 50 SCoins",
                   "Hora extra no laboratório - 100 SCoins", "Desconto na mensalidade - 500 SCoins"]
    return render_template("dashboard_aluno.html", scoins=saldo_scoins, desafios=desafios, recompensas=recompensas)

@app.route("/pessoas")
def pessoas():
    return render_template("pessAlun.html")


if __name__ == "__main__":
    app.run(debug=True)


