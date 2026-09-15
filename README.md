# =====================================================================
# AGENTE DE APRENDIZAJE AVANZADO (Q-LEARNING EN UN ENTORNO GRIDWORLD)
# =====================================================================
# Este agente supera el ejemplo básico al incorporar:
# 1. Múltiples estados (un entorno de cuadrícula 4x4).
# 2. Política Epsilon-Greedy (balance entre exploración y explotación).
# 3. Factor de descuento (gamma) para valorar recompensas futuras.
# 4. Bucle de entrenamiento por episodios con interacción dinámica.
# =====================================================================


class QLearningAgent:

  def __init__(
      self,
      acciones,
      alfa=0.1,
      gamma=0.9,
      epsilon=1.0,
      epsilon_min=0.01,
      epsilon_decay=0.995,
  ):
    self.acciones = acciones
    self.alfa = alfa  # Tasa de aprendizaje
    self.gamma = gamma  # Factor de descuento
    self.epsilon = epsilon  # Tasa de exploración inicial
    self.epsilon_min = epsilon_min
    self.epsilon_decay = epsilon_decay

    # Tabla Q: Mapea cada par (estado, acción) a un valor numérico Q(s, a)
    self.q_table = {}

  def obtener_q(self, estado, accion):
    # Si el estado-acción no ha sido visitado, inicializamos en 0.0
    return self.q_table.get((estado, accion), 0.0)

  def elegir_accion(self, estado):
    # Política Epsilon-Greedy: Exploración vs Explotación
    if random.uniform(0, 1) < self.epsilon:
      return random.choice(self.acciones)  # Exploración (acción aleatoria)

    # Explotación (elegir la mejor acción conocida para el estado actual)
    valores_acciones = [self.obtener_q(estado, a) for a in self.acciones]
    max_valor = max(valores_acciones)

    # Si hay múltiples acciones con el mismo valor máximo, rompemos el empate al azar
    mejores_acciones = [
        a for a, v in zip(self.acciones, valores_acciones) if v == max_valor
    ]
    return random.choice(mejores_acciones)

  def actualizar(self, estado, accion, recompensa, siguiente_estado):
    # Obtener el valor Q actual
    q_actual = self.obtener_q(estado, accion)

    # Estimar el valor máximo futuro para el siguiente estado
    max_q_siguiente = max(
        [self.obtener_q(siguiente_estado, a) for a in self.acciones]
    )

    # Ecuación de actualización de Q-Learning (Bellman)
    # Q(s,a) = Q(s,a) + alpha * [recompensa + gamma * max(Q(s',a')) - Q(s,a)]
    error = recompensa + (self.gamma * max_q_siguiente) - q_actual
    self.q_table[(estado, accion)] = q_actual + (self.alfa * error)

  def reducir_epsilon(self):
    if self.epsilon > self.epsilon_min:
      self.epsilon *= self.epsilon_decay


# =====================================================================
# ENTORNO: GRIDWORLD (MUNDO DE CUADRÍCULA)
# =====================================================================
class GridWorld:

  def __init__(self):
    self.filas = 4
    self.columnas = 4
    self.inicio = (0, 0)
    self.meta = (3, 3)
    self.trampa = (1, 1)
    self.estado_actual = self.inicio

  def reiniciar(self):
    self.estado_actual = self.inicio
    return self.estado_actual

  def paso(self, accion):
    x, y = self.estado_actual

    # Definir movimientos
    if accion == "ARRIBA":
      x = max(0, x - 1)
    elif accion == "ABAJO":
      x = min(self.filas - 1, x + 1)
    elif accion == "IZQUIERDA":
      y = max(0, y - 1)
    elif accion == "DERECHA":
      y = min(self.columnas - 1, y + 1)

    self.estado_actual = (x, y)

    # Calcular recompensas y condiciones de terminación
    if self.estado_actual == self.meta:
      return self.estado_actual, 10.0, True  # Recompensa alta por llegar a la meta
    elif self.estado_actual == self.trampa:
      return (
          self.estado_actual,
          -10.0,
          True,
      )  # Penalización alta por caer en trampa
    else:
      return (
          self.estado_actual,
          -0.1,
          False,
      )  # Pequeño costo por paso para fomentar rutas cortas


# =====================================================================
# ENTRENAMIENTO DEL AGENTE
# =====================================================================
acciones_disponibles = ["ARRIBA", "ABAJO", "IZQUIERDA", "DERECHA"]
agente = QLearningAgent(acciones=acciones_disponibles)
entorno = GridWorld()

episodios = 500

print("Iniciando entrenamiento del agente en GridWorld...")
for episodio in range(episodios):
  estado = entorno.reiniciar()
  terminado = False

  while not terminado:
    accion = agente.elegir_accion(estado)
    siguiente_estado, recompensa, terminado = entorno.paso(accion)

    agente.actualizar(estado, accion, recompensa, siguiente_estado)
    estado = siguiente_estado

  agente.reducir_epsilon()

print("¡Entrenamiento finalizado!\n")

# =====================================================================
# PRUEBA DEL AGENTE ENTRENADO
# =====================================================================
print("Probando el comportamiento del agente tras el aprendizaje:")
estado = entorno.reiniciar()
terminado = False
pasos = 0
camino = [estado]

while not terminado and pasos < 20:
  # En la fase de prueba, explotamos al máximo el conocimiento (epsilon = 0)
  agente.epsilon = 0
  accion = agente.elegir_accion(estado)
  estado, _, terminado = entorno.paso(accion)
  camino.append(estado)
  pasos += 1

print(f"Camino seguido por el agente: {camino}")
if camino[-1] == entorno.meta:
  print("¡El agente logró llegar a la meta con éxito!")
else:
  print("El agente no completó el objetivo en esta prueba.")
