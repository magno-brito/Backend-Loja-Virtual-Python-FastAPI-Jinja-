# Backend da Loja Virtual
### Magno Leal de Brito Junior e Róger Corrente Pinto

Para a realização do trabalho foi necessário mudar o arquivo admin_routes.py. Não havia o endpoint obter_usuarios. Criamos este endpoint para ser utilizado. Abaixo segue uma parte do código modificado.
```
@router.get("/obter_usuarios")
async def obter_usuarios():
    await asyncio.sleep(1)
    usuarios = UsuarioRepo.obter_todos_por_perfil()
    return usuarios

```

Usamos o método obter_todos_por_perfil() pois ele retorna todos os usuários com todos os seus atributos. Neste trabalho utilizamos apenas os atributos id, nome, email e telefone.
