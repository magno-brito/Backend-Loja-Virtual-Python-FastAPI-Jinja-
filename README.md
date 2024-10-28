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

Usamos o método obter_todos_por_perfil() pois ele retorna todos os usuários com todos os seus atributos. Neste trabalho utilizamos apenas os atributos id, nome, email e telefone. Para a exclusão do usuário foi necessária a criação da classe DTO IdUsuarioDTO

```
class IdUsuarioDto(BaseModel):
    id_usuario: int

    @field_validator("id_usuario")
    def validar_id_usuario(cls, v):
        msg = is_greater_than(v, "Id do Usuario", 0)
        if msg: raise ValueError(msg)
        return v

```

Esta classe foi utilizada no endpoint excluir_usuario que também precisamos criar para que, ao clicar no no botão, o usuário possa ser excluído conforme mostra o código abaixo.

```
@router.post("/excluir_usuario", status_code=204)
async def excluir_usuario(inputDto: IdUsuarioDto):
    if UsuarioRepo.excluir(inputDto.id_usuario): return None
    pd = ProblemDetailsDto("int", f"O usuario com id <b>{inputDto.id_usuario}</b> não foi encontrado.", "value_not_found", ["body", "id_produto"])
    return JSONResponse(pd.to_dict(), status_code=404)

```
