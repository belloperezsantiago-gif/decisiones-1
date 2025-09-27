import flet as ft

def main(page: ft.Page):
    page.title = "Aventura en la Isla"
    page.vertical_alignment = "center"
    page.horizontal_alignment = "center"

    
    estado = {"pregunta": "inicio"}

    
    decisiones = {
        "inicio": {
            "texto": "Despiertas en una isla misteriosa 🏝️. ¿Qué haces?",
            "opciones": {
                "Explorar la selva 🌳": "selva",
                "Ir a la playa 🏖️": "playa"
            }
        },
        "selva": {
            "texto": "Te adentras en la selva. ¿Qué decides?",
            "opciones": {
                "Seguir el río 💧": "rio",
                "Trepas un árbol 🌴": "arbol"
            }
        },
        "rio": {
            "texto": "Sigues el río y encuentras un pueblo. ¡Has sido rescatado! 🎉",
            "opciones": {}
        },
        "arbol": {
            "texto": "Caes del árbol y te lastimas gravemente... Final malo ☠️",
            "opciones": {}
        },
        "playa": {
            "texto": "Llegas a la playa. ¿Qué decides?",
            "opciones": {
                "Construir una balsa 🛶": "balsa",
                "Buscar comida 🍌": "comida"
            }
        },
        "balsa": {
            "texto": "Construyes una balsa y escapas de la isla. ¡Final bueno! 🎉",
            "opciones": {}
        },
        "comida": {
            "texto": "No encuentras comida y mueres de hambre... Final malo ☠️",
            "opciones": {}
        }
    }

    
    pregunta_texto = ft.Text(size=20, text_align="center")

    
    botones = ft.Column()

    
    def mostrar_pregunta(paso):
        estado["pregunta"] = paso
        pregunta = decisiones[paso]
        pregunta_texto.value = pregunta["texto"]
        botones.controls.clear()

        if pregunta["opciones"]:
            for texto_op, destino in pregunta["opciones"].items():
                botones.controls.append(ft.ElevatedButton(text=texto_op, on_click=lambda e, d=destino: mostrar_pregunta(d)))
        else:
            # Final → Mostrar botón reiniciar
            botones.controls.append(ft.ElevatedButton(text="🔄 Reiniciar", on_click=lambda e: mostrar_pregunta("inicio")))

        page.update()

    
    mostrar_pregunta("inicio")

    
    page.add(
        ft.Column(
            controls=[pregunta_texto, botones],
            horizontal_alignment="center",
            alignment="center"
        )
    )

ft.app(target=main)
