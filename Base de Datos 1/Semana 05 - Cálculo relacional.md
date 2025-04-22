

Ejercicio de ejemplo:
- **Server**(_name_, image, state, region)
- **Channel**(_name_, isprivate, type, *S.name*)
- **User**(_username_, fullname, rolename, *S.name*)
- **message**(_id_, C.name, creationtime, text, U.username, S.name)

1. Muestre aquel servidor que tenga la mayor cantidad de mensajes en total

$$R_1 \leftarrow \text{s.name} \gamma_{\text{count}}(id)(M)$$

$$R_2 \leftarrow \rho_{\text{count / count-message}}(R_1)$$

$$R_3 \leftarrow \gamma_{\text{max(count-message)}}(R_2)$$

$$R_4 \leftarrow R_3$$