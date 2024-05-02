
## Evidencia del cambio
> Ponga aquí evidencia con imágenes y fragmento de código

#### Archivo Json guarda 4 jugadores
La función que fue editada para que mostrara la puntuacion de 4 jugadores fue leaderboard:
```python
def Leaderboard(what_to_do):
    """
    Gestiona las operaciones del tablero de líderes como crear, escribir y leer los datos del jugador.
    
    Args:
    what_to_do (str): Define la operación a realizar con el tablero de líderes ('create', 'write', 'read').
    """
    if what_to_do == 'create':
        if mystate.GameDetails[3] != '' and not os.path.isfile(vpth + 'leaderboard.json'):
            json.dump({}, open(vpth + 'leaderboard.json', 'w'))

    elif what_to_do == 'write':
        if mystate.GameDetails[3] != '' and os.path.isfile(vpth + 'leaderboard.json'):
            leaderboard = json.load(open(vpth + 'leaderboard.json'))
            leaderboard[str(len(leaderboard) + 1)] = {'NameCountry': mystate.GameDetails[3], 'HighestScore': mystate.myscore}
            # Ordenar el leaderboard por HighestScore de forma descendente
            leaderboard = dict(sorted(leaderboard.items(), key=lambda item: item[1]['HighestScore'], reverse=True))

            # Mantener solo los top 4 jugadores en el leaderboard
            if len(leaderboard) > 4:
                while len(leaderboard) > 4:
                    leaderboard.popitem()  # Elimina el último elemento

            json.dump(leaderboard, open(vpth + 'leaderboard.json', 'w'))  # Escribir el leaderboard actualizado en el archivo JSON

    elif what_to_do == 'read':
        if os.path.isfile(vpth + 'leaderboard.json'):
            leaderboard = json.load(open(vpth + 'leaderboard.json'))
            leaderboard = dict(sorted(leaderboard.items(), key=lambda item: item[1]['HighestScore'], reverse=True))

            # Establecer columnas para mostrar los jugadores
            sc0, sc1, sc2, sc3, sc4 = st.columns((2,3,3,3, 3))
            rank = 0
            sc0.write('🏆 Past Winners:')
            for vkey in leaderboard.keys():
                rank += 1
                if rank == 1:
                    sc1.write(f"🥇 | {leaderboard[vkey]['NameCountry']}: {leaderboard[vkey]['HighestScore']}")
                elif rank == 2:
                    sc2.write(f"🥈 | {leaderboard[vkey]['NameCountry']}: {leaderboard[vkey]['HighestScore']}")
                elif rank == 3:
                    sc3.write(f"🥉 | {leaderboard[vkey]['NameCountry']}: {leaderboard[vkey]['HighestScore']}")
                elif rank == 4:
                    sc4.write(f"🏅 | {leaderboard[vkey]['NameCountry']}: {leaderboard[vkey]['HighestScore']}")
```

#### Interfa gráfica muestra cuatro jugadores

#### Usuario pierde el juego cuando supera un máximo posible de fallos.



## Encuesta de la experiencia
Por favor, responde las siguientes preguntas basadas en tu experiencia modificando el código para incluir cuatro personas en el leaderboard en lugar de tres.

**Nombre:** Juliana Sanchez

#### 1. ¿Cuánto tiempo te llevó entender las secciones del código relacionada con el leaderboard?
- [ ] Menos de 10 minutos
- [ ] Entre 10 y 30 minutos
- [x] Entre 30 minutos y 1 hora
- [ ] Más de 1 hora

#### 2. ¿Cuánto tiempo te llevó entender las secciones del código relacionada con hacer que el usuario pierda si supera x cantidad de turnos?
- [ ] Menos de 10 minutos
- [ ] Entre 10 y 30 minutos
- [ ] Entre 30 minutos y 1 hora
- [x] Más de 1 hora

#### 3. ¿Consideras que estaba documentada la lógica en el código para facilitar el cambio?
- [ ] Sí
- [x] No

#### 4. ¿Te pareció fácil identificar dónde y qué cambios realizar para aumentar el número de personas en el leaderboard de 3 a 4?
- [ ] Muy fácil
- [ ] Algo fácil
- [x] Algo difícil
- [ ] Muy difícil


#### 5. ¿Te pareció fácil identificar dónde y qué cambios realizar para agregar la lógica de perder el juego?
- [ ] Muy fácil
- [ ] Algo fácil
- [x] Algo difícil
- [ ] Muy difícil


#### 5. ¿Qué tan seguro te sientes de que tus cambios no introdujeron errores en otras áreas del código?
- [ ] Muy seguro
- [x] Moderadamente seguro
- [ ] Poco seguro
- [ ] Nada seguro

#### 6. Después de realizar los cambios, ¿cuánto tiempo te tomó verificar que el cambio funcionó como se esperaba?
- [ ] Menos de 10 minutos
- [ ] Entre 10 y 30 minutos
- [ ] Entre 30 minutos y 1 hora
- [x] Más de 1 hora

#### 7. ¿Qué estrategia usaste para verificar que no habían problemas en el código fuente?

Intentaba compilar el proyecto constantemente para verificiar que streamlit no me mostrara nigun tipo de error

#### 8. ¿Te enfrentaste a algún problema mientras intentabas realizar los cambios? Si es así, ¿cómo lo resolviste?
- [ ] No enfrenté problemas
- [ ] Revisé la documentación del código
- [x] Busqué ayuda de un compañero o en línea
- [ ] Otro (especificar)

Para el uso de algunas sintaxis nuevas, tuve que buscar su uso en internet debido a que eran propiedades muy especificas de algunas de las librerias utilizadas en el proyecto.