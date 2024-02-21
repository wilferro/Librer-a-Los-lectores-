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
cantidad = 3
precio = 90.00
tipo_libro = 1  # Ficción
descuento = calcular_descuento(cantidad, tipo_libro)
importe_neto = calcular_importe_neto(cantidad, precio, descuento)
print("Importe Neto:", importe_neto)
