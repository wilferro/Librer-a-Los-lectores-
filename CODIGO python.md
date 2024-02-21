import pyodbc

# Establecer la conexión con la base de datos
conn=pyodbc.connect(
"Driver=[SQL Server Native Client 12.0);"
"Server=localhost;"
"Database=BD_PRACTICA;"
"trusted connection-yes;"
)
# Función para registrar un nuevo cliente
def registrar_cliente(nombre, genero):
    cursor = conn.cursor()
    cursor.execute("INSERT INTO Clientes (Nombre, Genero) VALUES (?, ?)", (nombre, genero))
    conn.commit()
    print("Cliente registrado correctamente.")

# Función para registrar una nueva venta
def registrar_venta(id_cliente, id_libro, cantidad, importe_bruto, monto_descuento, importe_neto):
    cursor = conn.cursor()
    cursor.execute("INSERT INTO Ventas (ID_Cliente, ID_Libro, Cantidad, Importe_Bruto, Monto_Descuento, Importe_Neto) VALUES (?, ?, ?, ?, ?, ?)",
                   (id_cliente, id_libro, cantidad, importe_bruto, monto_descuento, importe_neto))
    conn.commit()
    print("Venta registrada correctamente.")

# Calcular el porcentaje de descuento en función de la cantidad y el tipo de libro
def calcular_descuento(cantidad, tipo_libro):
    if tipo_libro == 1:  # Ficción
        if cantidad <= 2:
            return 0.05
        elif cantidad <= 6:
            return 0.06
        elif cantidad > 7:
            return 0.08
        else:
            return 0.02
    elif tipo_libro == 2:  # Novelas
        if cantidad <= 2:
            return 0.08
        elif cantidad <= 6:
            return 0.16
        elif cantidad > 7:
            return 0.32
        else:
            return 0.08
    elif tipo_libro == 3:  # Cuentos
        if cantidad <= 2:
            return 0.09
        elif cantidad <= 6:
            return 0.16
        elif cantidad > 7:
            return 0.36
        else:
            return 0.32
    elif tipo_libro == 4:  # Física Cuántica
        if cantidad <= 2:
            return 0.2
        elif cantidad <= 6:
            return 0.2
        elif cantidad > 7:
            return 0.4
        else:
            return 0.2

# Calcular el importe neto de la venta
def calcular_importe_neto(cantidad, precio, descuento):
    importe_bruto = cantidad * precio
    monto_descuento = importe_bruto * descuento
    importe_neto = importe_bruto - monto_descuento
    return importe_neto

# Ejemplo de uso
if __name__ == "__main__":
    # Registro de un nuevo cliente
    nombre = input("Ingrese el nombre del cliente: ")
    genero = input("Ingrese el género del cliente: ")
    registrar_cliente(nombre, genero)

    # Registro de una nueva venta (debes completar los datos de la venta)
    id_cliente = int(input("Ingrese el ID del cliente: "))
    id_libro = int(input("Ingrese el ID del libro: "))
    cantidad = int(input("Ingrese la cantidad de libros: "))
    precio = float(input("Ingrese el precio del libro: "))
    tipo_libro = int(input("Ingrese el tipo de libro (1-Ficción / 2-Novelas / 3-Cuentos / 4-Física Cuántica): "))
    descuento = calcular_descuento(cantidad, tipo_libro)
    importe_neto = calcular_importe_neto(cantidad, precio, descuento)
    print("Importe Neto:", importe_neto)
    registrar_venta(id_cliente, id_libro, cantidad, cantidad * precio, cantidad * precio * descuento, importe_neto)

