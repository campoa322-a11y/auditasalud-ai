import streamlit as st

# Configuración de la página
st.set_page_config(
    page_title="AuditaSalud AI - Gestión de Glosas",
    page_icon="🏥",
    layout="wide"
)

# Título y Encabezado
st.title("🏥 AuditaSalud AI")
st.subtitle("Asistente Inteligente para la Contestación Estratégica de Glosas por Pertinencia Médica")
st.markdown("---")

# Barra lateral informativa
with st.sidebar:
    st.header("⚙️ Configuración")
    st.info("Plataforma diseñada para coordinadores de auditoría médica y analistas de cuentas médicas.")
    st.markdown("**Versión:** 1.0 - Prototipo Funcional")
    st.markdown("**Modelo Base:** GPT-4o / Claude 3.5 Sonnet")

# Formulario de entrada de la glosa
st.header("📋 Formulario de Registro de Glosa")

col1, col2 = st.columns(2)

with col1:
    procedimiento = st.text_input("Procedimiento / Servicio Glosado:", "Resonancia Magnética de Cerebro Simple")
    cie10 = st.text_input("Código y Diagnóstico CIE-10:", "G44.2 - Cefalea tensional crónica")
    motivo_glosa = st.text_area("Motivo de la Glosa (Expuesto por la EPS):", "No se evidencia pertinencia médica en historia clínica. No agota manejo de primera línea antes del estudio de alta complejidad.")

with col2:
    historia_clinica = st.text_area("Resumen / Soportes de Historia Clínica:", "Paciente femenina de 34 años con cefalea holocraneana de 8 meses de evolución, intensidad 8/10, refractaria a tratamiento farmacológico con AINEs y moduladores del dolor. Presenta episodios nocturnos que alteran el sueño y alteración neurológica leve en la marcha detectada en último examen físico.", height=185)

# Botón para generar la respuesta
if st.button("🚀 Generar Contestación Técnico-Médica", type="primary"):
    if procedimiento and cie10 and motivo_glosa and historia_clinica:
        st.markdown("---")
        st.subheader("📑 Borrador de Respuesta a la Glosa Generado")
        
        # Simulación de respuesta estructurada según el Prompt
        respuesta_plantilla = f"""
**ASUNTO:** Respuesta y Solicitud de Levantamiento de Glosa por Pertinencia Médica  
**SERVICIO GLOSADO:** {procedimiento}  
**DIAGNÓSTICO:** {cie10}  

---

### 1. MOTIVO DE LA OBJECIÓN
La entidad pagadora argumenta la glosa bajo la premisa: *"{motivo_glosa}"*.

### 2. FUNDAMENTACIÓN TÉCNICO-MÉDICA (SUSTENTO DE PERTINENCIA)
Revisados los antecedentes clínicos del usuario, se ratifica la pertinencia médica del servicio brindado con base en los siguientes criterios clínicos e indicadores de riesgo:

* **Evolución y Refractariedad:** La paciente presenta un cuadro clínico de cefalea crónica de 8 meses de evolución, habiendo agotado esquemas farmacológicos de primera línea sin respuesta favorable.
* **Criterios de Cefalea Red Flag (Signos de Alarma):** La presencia de cefalea nocturna que interrumpe el sueño asociada a focalización o alteración en el examen físico (marcha) constituye un criterio médico absoluto para indicación de imagenología neurodiagnóstica de alta complejidad, de acuerdo con la Guía de Práctica Clínica para el Manejo de Cefaleas.
* **Progresión Diagnóstica:** El estudio **{procedimiento}** resulta indispensable para descartar patología estructural subyacente de origen neurológico, garantizando la seguridad del paciente y la oportunidad en el diagnóstico.

### 3. PETICIÓN CONCRETA
Por lo expuesto y con fundamento en los soportes clínicos adjuntos, solicitamos de manera formal el **LEVANTAMIENTO TOTAL DE LA GLOSA** y la posterior autorización de pago de la factura correspondiente al procedimiento **{procedimiento}**.
        """
        
        st.success("¡Contestación generada exitosamente!")
        st.markdown(respuesta_plantilla)
        
        # Botón para descargar el resultado
        st.download_button(
            label="📄 Descargar Respuesta (Texto)",
            data=respuesta_plantilla,
            file_name="Respuesta_Glosa_AuditaSalud.txt",
            mime="text/plain"
        )
    else:
        st.warning("Por favor, diligencie todos los campos antes de generar la respuesta.")