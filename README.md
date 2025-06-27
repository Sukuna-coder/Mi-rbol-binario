class Nodo:
    def __init__(self, valor):
        self.valor = valor
        self.izquierda = None
        self.derecha = None

class ArbolBinario:
    def __init__(self):
        self.raiz = None

    def insertar(self, valor):
        if self.raiz is None:
            self.raiz = Nodo(valor)
        else:
            self._insertar_recursivo(self.raiz, valor)

    def _insertar_recursivo(self, nodo_actual, valor):
        if valor < nodo_actual.valor:
            if nodo_actual.izquierda is None:
                nodo_actual.izquierda = Nodo(valor)
            else:
                self._insertar_recursivo(nodo_actual.izquierda, valor)
        else: # valor >= nodo_actual.valor (maneja duplicados o mayores a la derecha)
            if nodo_actual.derecha is None:
                nodo_actual.derecha = Nodo(valor)
            else:
                self._insertar_recursivo(nodo_actual.derecha, valor)

    def recorrido_inorder(self):
        elementos = []
        self._inorder_recursivo(self.raiz, elementos)
        return elementos

    def _inorder_recursivo(self, nodo_actual, elementos):
        if nodo_actual:
            self._inorder_recursivo(nodo_actual.izquierda, elementos)
            elementos.append(nodo_actual.valor)
            self._inorder_recursivo(nodo_actual.derecha, elementos)

    def recorrido_preorder(self):
        elementos = []
        self._preorder_recursivo(self.raiz, elementos)
        return elementos

    def _preorder_recursivo(self, nodo_actual, elementos):
        if nodo_actual:
            elementos.append(nodo_actual.valor)
            self._preorder_recursivo(nodo_actual.izquierda, elementos)
            self._preorder_recursivo(nodo_actual.derecha, elementos)

    def recorrido_posorder(self):
        elementos = []
        self._posorder_recursivo(self.raiz, elementos)
        return elementos

    def _posorder_recursivo(self, nodo_actual, elementos):
        if nodo_actual:
            self._posorder_recursivo(nodo_actual.izquierda, elementos)
            self._posorder_recursivo(nodo_actual.derecha, elementos)
            elementos.append(nodo_actual.valor)

# --- Programa Principal ---
if __name__ == "__main__":
    arbol = ArbolBinario()
    print("--- Construcción del Árbol Binario ---")
    print("Ingresa los elementos que deseas añadir al árbol (escribe 'fin' para terminar):")

    while True:
        entrada = input("Elemento a insertar: ")
        if entrada.lower() == 'fin':
            break
        try:
            valor = int(entrada)
            arbol.insertar(valor)
            print(f"'{valor}' insertado.")
        except ValueError:
            print("Entrada inválida. Por favor, ingresa un número entero o 'fin'.")

    print("\n--- Recorridos del Árbol ---")
    print(f"Recorrido Inorder (Ordenado): {arbol.recorrido_inorder()}")
    print(f"Recorrido Preorder (Raíz-Izquierda-Derecha): {arbol.recorrido_preorder()}")
    print(f"Recorrido Posorder (Izquierda-Derecha-Raíz): {arbol.recorrido_posorder()}")
