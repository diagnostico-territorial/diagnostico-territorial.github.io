# diagnostico-territorial.github.io

Publica em <https://diagnostico-territorial.github.io/> a interface do **Agente Diagnóstico Territorial da Força de Trabalho
na Saúde**. O código vem do repositório público
[gustavohoff1987/Teste-Agente](https://github.com/gustavohoff1987/Teste-Agente), ramo `implantacao/cloud-run-pages`. A
interface chama o serviço de análise no Google Cloud Run, o mesmo da publicação em
<https://gustavohoff1987.github.io/Teste-Agente/>.

## Como a publicação acontece

- `origem.txt` fixa o commit do Teste-Agente que é publicado: só o SHA completo.
- `.github/workflows/publicar.yml` só roda com o envio de uma etiqueta `publicacao-pages-*`. A execução tem três etapas:
  1. **Conferências:** o repositório público, o ambiente `github-pages` com revisor e só essa regra de etiqueta, o commit da
     etiqueta no `main` e a origem. A origem confere se o commit pertence ao ramo `implantacao/cloud-run-pages` e se o CI do
     Teste-Agente terminou em sucesso nele.
  2. **Build:** constrói a interface na raiz (`ADT_BASE_DA_PAGINA=/`), com o endereço do serviço da variável
     `VITE_API_BASE_URL`, e confere o padrão de chave do Google no build.
  3. **Publicação:** no ambiente `github-pages`, depois da aprovação manual.
- As conferências usam as cópias destes scripts guardadas aqui, em `.github/scripts/`, iguais às do Teste-Agente no commit de
  `origem.txt`. Assim, elas não dependem do código que conferem.
- Não há credencial entre os repositórios: o Teste-Agente é público e só é lido.

O registro das operações está em `Docs/implantacao/` do Teste-Agente (roteiro, operações M-0 a M-5; relatório, seção O).
