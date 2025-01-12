```ad-definition
Una ecuación diferencial de primer orden de la forma
$$\frac{dy}{dx} = g(x)h(y)$$
se dice que es separable o tiene variables separables.
```

Para resolver una ecuación diferencial de variables separables se realiza lo siguiente:

- **Paso 1**: Separar las variables
$$\frac{dy}{h(y)} = g(x)dx$$
- **Paso 2**: Aplicar integrales en ambas partes de la ecuación anterior
$$\int\frac{dy}{h(y)} = \int g(x)dx$$
- **Paso 3**: Integrar
$$H(y) = G(x) + C$$

## Pérdida de solución

Cuando $r$ es cero de $h(y)$, entonces $y = r$ es también una solución de la ecuación (llamada **solución singular**). Sin embargo, esta solución no aparecerá en la integración.

```ad-note
Esta perdida de solución ocurre pues al resolver la ecuación diferencial realizamos una división entre $h(y)$, para lo cual se asume que $h(y) \neq 0$.
```
## Soluciones definidas por integrales

Si $g$ es una función continua en el intervalo abierto $I$ que contiene a $x_0$, entonces el problema de valor inicial
$$\frac{dy}{dx} = g(x), \quad g(x_0) = y_0$$
tiene por solución
$$y(x) = y_0 + \int_{x_0}^xg(t)dt$$
