https://masteryink-ni.vercel.app/https://masteryink-ni.vercel.app/https://masteryink-ni.vercel.app/import streamlit as st
import json
import os

# Configuración de página
st.set_page_config(
    page_title="Mastery Ink | Aula Virtual & Bioseguridad MINSA",
    page_icon="🎨",
    layout="wide"
)

# Archivo de configuración local para guardar contraseñas
CONFIG_FILE = "app_config.json"

def load_config():
    if os.path.exists(CONFIG_FILE):
        try:
            with open(CONFIG_FILE, "r") as f:
                return json.load(f)
        except Exception:
            pass
    return {
        "student_password": "MASTERY_ALUMNO",
        "founder_password": "MASTERY_FUNDADOR"
    }

def save_config(config):
    with open(CONFIG_FILE, "w") as f:
        json.dump(config, f, indent=4)

# Cargar credenciales
config = load_config()

# Estado de sesión para login
if "authenticated" not in st.session_state:
    st.session_state["authenticated"] = False
if "role" not in st.session_state:
    st.session_state["role"] = None

# --- PANTALLA DE AUTENTICACIÓN ---
if not st.session_state["authenticated"]:
    st.title("🔒 Mastery Ink Perú — Acceso al Aula Virtual")
    st.subheader("Plataforma de Mentoría de Tatuaje Profesional & Bioseguridad MINSA")
    
    st.markdown("""
    Bienvenido a la plataforma privada de entrenamiento. Por favor, ingresa tu clave de acceso.
    """)
    
    col1, col2 = st.columns([2, 1])
    with col1:
        pwd_input = st.text_input("Contraseña de Acceso", type="password")
        btn_login = st.button("Ingresar al Aula")
        
        if btn_login:
            if pwd_input == config["student_password"]:
                st.session_state["authenticated"] = True
                st.session_state["role"] = "student"
                st.success("Acceso concedido como Alumno.")
                st.rerun()
            elif pwd_input == config["founder_password"]:
                st.session_state["authenticated"] = True
                st.session_state["role"] = "founder"
                st.success("Acceso concedido como Fundador/Administrador.")
                st.rerun()
            else:
                st.error("Contraseña incorrecta. Consulta con el fundador del programa.")
    st.stop()

# --- BARRA LATERAL (MENÚ Y CONTROL DE FUNDADOR) ---
st.sidebar.image("https://via.placeholder.com/150x50?text=MASTERY+INK", use_container_width=True)
st.sidebar.title("📌 Menú del Aula Virtual")

# Gestión de Contraseñas (Sólo Fundador)
if st.session_state["role"] == "founder":
    st.sidebar.markdown("---")
    st.sidebar.subheader("👑 Panel del Fundador")
    st.sidebar.info("Modo Administrador Activo")
    
    with st.sidebar.expander("🔑 Cambiar Contraseñas"):
        new_student_pwd = st.text_input("Nueva Clave Alumnos", value=config["student_password"], type="password")
        new_founder_pwd = st.text_input("Nueva Clave Fundador", value=config["founder_password"], type="password")
        if st.button("Guardar Nuevas Claves"):
            config["student_password"] = new_student_pwd
            config["founder_password"] = new_founder_pwd
            save_config(config)
            st.success("¡Contraseñas actualizadas con éxito!")

if st.sidebar.button("🚪 Cerrar Sesión"):
    st.session_state["authenticated"] = False
    st.session_state["role"] = None
    st.rerun()

st.sidebar.markdown("---")
menu_option = st.sidebar.radio(
    "Navegación",
    [
        "📚 Módulos del Curso",
        "📋 Checklist de Mesa Estéril",
        "🎴 Tarjetas de Repaso (Flashcards)",
        "📝 Cuestionario de Bioseguridad (Quiz)",
        "💰 Simulador de Presupuestos (S/)",
        "📁 Biblioteca de Recursos Studio"
    ]
)

# --- SECCIÓN 1: MÓDULOS DEL CURSO ---
if menu_option == "📚 Módulos del Curso":
    st.header("🎓 Módulos Curriculares — Mastery Ink Perú")
    
    tab1, tab2, tab3, tab4, tab5, tab6 = st.tabs([
        "Mod 1: Bioseguridad",
        "Mod 2: Máquinas Pen",
        "Mod 3: Line Work",
        "Mod 4: Sombras",
        "Mod 5: Cuidado",
        "Mod 6: Marketing"
    ])
    
    with tab1:
        st.subheader("Módulo 1: Bioseguridad y Normas MINSA / DIGESA")
        st.markdown("""
        **Normativa NTS Nº 144-MINSA/2018/DIGESA para gestión de residuos:**
        * **🔴 Bolsa Roja (Biocontaminados):** Guantes de nitrilo, gasas, algodón y materiales con fluidos/sangre.
        * **🟡 Caja Rígida Hermética (Punzocortantes):** Descarte obligatorio de agujas, cartuchos usados y bisturíes.
        * **⬛ Bolsa Negra (Comunes):** Papel, cartón y empaques limpios.
        
        **Asepsia:** Desinfección con alcohol de 70°/90° y uso de barreras de protección plastificadas (*film*) para la máquina Pen y cableado.
        """)
    
    with tab2:
        st.subheader("Módulo 2: Calibración de Máquinas Pen y Cartuchos")
        st.markdown("""
        * **Mecánica y Stroke:** Elección del recorrido según estilo (línea fina vs. relleno).
        * **Agujas y Cartuchos:** Diferencias entre 3RL, 7RL, 11RM (Magnum) y ajuste de la membrana de seguridad.
        * **Voltaje:** Regulación de la fuente inalámbrica según la resistencia y densidad de la piel.
        """)

    with tab3:
        st.subheader("Módulo 3: Técnica de Line Work (Línea Fina)")
        st.markdown("""
        * **Anatomía Cutánea:** Inyección precisa en la **dermis** para evitar la expansión de tinta (*blowout*).
        * **Biomecánica:** Control de pulso, velocidad de mano, inclinación del cartucho a 45°-70° y firmeza de apoyo.
        """)

    with tab4:
        st.subheader("Módulo 4: Sombras Black & Grey y Dilución Sumie")
        st.markdown("""
        * **Escala Sumie:** Preparación de copas (*caps*) con gradación de gotas de tinta negra y agua destilada/diluyente.
        * **Técnica de Péndulo:** Movimientos suaves para lograr degradados homogéneos sin traumatizar la piel.
        """)

    with tab5:
        st.subheader("Módulo 5: Cuidados Post-Tatuaje y Cicatrización")
        st.markdown("""
        * **Aislamiento:** Uso de parches de curación dermoprotectores de film transparente.
        * **Recomendaciones para el Cliente:** Limpieza con jabón neutro, hidratación y prevención de infecciones.
        """)

    with tab6:
        st.subheader("Módulo 6: Marketing y Captación de Clientes en Perú")
        st.markdown("""
        * **Redes Sociales:** Producción de contenido para TikTok e Instagram con iluminación polarizada.
        * **Estrategia Comercial:** Protocolo de cotización rápida por WhatsApp para convertir consultas en citas.
        """)

# --- SECCIÓN 2: CHECKLIST DE MESA ESTÉRIL ---
elif menu_option == "📋 Checklist de Mesa Estéril":
    st.header("📋 Lista de Verificación — Mesa Estéril (DIGESA)")
    st.info("Marca cada paso antes de iniciar tu sesión de tatuaje para garantizar el cumplimiento sanitario.")
    
    st.checkbox("1. Desinfección de la mesa de trabajo con alcohol al 70%/90° o amonio cuaternario")
    st.checkbox("2. Colocación del campo quirúrgico impermeable sobre la mesa")
    st.checkbox("3. Envoltura plastificada (Film de protección) en la máquina Pen, fuente y cables")
    st.checkbox("4. Posicionamiento de Caja Rígida Hermética para agujas y punzocortantes a la mano")
    st.checkbox("5. Posicionamiento de Bolsa Roja para residuos biocontaminados")
    st.checkbox("6. Montaje de caps con pigmentos y vaselina aplicada con bajalenguas descartable")
    st.checkbox("7. Uso de EPP completo: Guantes de nitrilo, mascarilla y mandilón")

# --- SECCIÓN 3: FLASHCARDS ---
elif menu_option == "🎴 Tarjetas de Repaso (Flashcards)":
    st.header("🎴 Tarjetas Interactivas de Repaso")
    
    cards = [
        {"q": "¿En qué contenedor se desechan las agujas y cartuchos usados?", "a": "En la Caja Rígida Hermética para punzocortantes (NTS Nº 144-MINSA)."},
        {"q": "¿En qué capa de la piel se debe inyectar el pigmento?", "a": "En la Dermis (profundidad de 1.5mm a 2mm aproximadamente)."},
        {"q": "¿Qué ocurre si se inyecta la tinta demasiado profundo en la hipodermis?", "a": "Se produce el efecto 'Blowout' (expansión o migración no deseada de la tinta)."},
        {"q": "¿Qué va en la Bolsa Roja según DIGESA?", "a": "Guantes con fluidos, gasas, algodón y materiales contaminados con sangre."}
    ]
    
    for i, card in enumerate(cards):
        with st.expander(f"Tarjeta {i+1}: {card['q']}"):
            st.write(f"**Respuesta:** {card['a']}")

# --- SECCIÓN 4: QUIZ ---
elif menu_option == "📝 Cuestionario de Bioseguridad (Quiz)":
    st.header("📝 Evaluación Rápida de Bioseguridad MINSA")
    
    q1 = st.radio("1. ¿Dónde deben descartarse los guantes usados con restos de sangre?", ["Bolsa Negra", "Bolsa Roja", "Caja Rígida"])
    q2 = st.radio("2. ¿Qué norma técnica del MINSA regula el manejo de residuos sólidos en salud en Perú?", ["NTS Nº 144-MINSA/2018/DIGESA", "Ley de Trabajo N° 29783", "Decreto Supremo 005-TR"])
    
    if st.button("Enviar Respuestas"):
        score = 0
        if q1 == "Bolsa Roja":
            score += 1
        if q2 == "NTS Nº 144-MINSA/2018/DIGESA":
            score += 1
        
        st.success(f"Puntaje obtenido: {score}/2")
        if score == 2:
            st.balloons()

# --- SECCIÓN 5: SIMULADOR ---
elif menu_option == "💰 Simulador de Presupuestos (S/)":
    st.header("💰 Simulador de Ingresos por Tatuaje en Perú")
    st.write("Calcula la rentabilidad de tus trabajos según las tarifas del mercado peruano.")
    
    cant_minimalistas = st.number_input("Tatuajes Minimalistas/Línea Fina por mes (S/ 80 avg)", min_value=0, value=10)
    cant_medianos = st.number_input("Tatuajes Medianos/Sombras por mes (S/ 250 avg)", min_value=0, value=4)
    cant_grandes = st.number_input("Piezas Grandes/Sesiones Completas por mes (S/ 600 avg)", min_value=0, value=2)
    
    ingreso_total = (cant_minimalistas * 80) + (cant_medianos * 250) + (cant_grandes * 600)
    costo_insumos = ingreso_total * 0.18 # Estimado de insumos y desechables
    ganancia_neta = ingreso_total - costo_insumos
    
    st.metric("Ingreso Bruto Estimado", f"S/ {ingreso_total:,.2f}")
    st.metric("Costo Estimado de Insumos (18%)", f"S/ {costo_insumos:,.2f}")
    st.metric("Ganancia Neta Mensual", f"S/ {ganancia_neta:,.2f}", delta="Rentable")

# --- SECCIÓN 6: BIBLIOTECA ---
elif menu_option == "📁 Biblioteca de Recursos Studio":
    st.header("📁 Materiales Complementarios")
    st.write("Accede a todos los materiales interactivos generados para el programa:")
    st.markdown("""
    * 📖 **Ebook Completo en PDF/Reporte:** Disponible en el panel Studio.
    * 📊 **Infografía de Mesa Estéril:** Disponible en el panel Studio.
    * 🎙️ **Audio Podcast de Repaso:** Disponible en el panel Studio.
    * 🎥 **Video Introductorio del Programa:** Disponible en el panel Studio.
    """)
