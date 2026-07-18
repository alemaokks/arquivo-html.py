from flask import Flask, request

app = Flask(__name__)

@app.route("/")
def calculadora():
    resultado = ""

    if "numero1" in request.args:
        numero1 = float(request.args.get("numero1"))
        numero2 = float(request.args.get("numero2"))
        operacao = request.args.get("operacao")

        if operacao == "+":
            resultado = numero1 + numero2

        elif operacao == "-":
            resultado = numero1 - numero2

        elif operacao == "*":
            resultado = numero1 * numero2

        elif operacao == "/":
            if numero2 == 0:
                resultado = "Erro: divisão por zero."
            else:
                resultado = numero1 / numero2

        elif operacao == "**":
            resultado = numero1 ** numero2

        elif operacao == "%":
            if numero2 == 0:
                resultado = "Erro: divisão por zero."
            else:
                resultado = numero1 % numero2

    return f"""
    <!DOCTYPE html>
    <html>
    <head>
        <title>Calculadora em Python</title>
    </head>
    <body>
        <h1>Calculadora</h1>

        <form>
            <input type="number" step="any" name="numero1" required>

            <select name="operacao">
                <option value="+">+</option>
                <option value="-">-</option>
                <option value="*">*</option>
                <option value="/">/</option>
                <option value="**">**</option>
                <option value="%">%</option>
            </select>

            <input type="number" step="any" name="numero2" required>

            <button type="submit">Calcular</button>
        </form>

        <h2>Resultado: {resultado}</h2>

    </body>
    </html>
    """

if __name__ == "__main__":
    app.run(debug=True)
