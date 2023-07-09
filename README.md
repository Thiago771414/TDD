# Boas práticas de arquitetura - Test-Driven Development (TDD):

O Test-Driven Development (TDD) é uma prática de desenvolvimento de software que envolve escrever testes antes de escrever o código de produção. O ciclo básico do TDD é composto por três etapas: escrever um teste automatizado que falha, escrever o código de produção para fazer o teste passar e, em seguida, refatorar o código para melhorar a qualidade.
Essa abordagem tem como objetivo garantir que cada funcionalidade do software seja testada de forma automatizada, o que aumenta a confiabilidade e a qualidade do código. Além disso, ao escrever os testes primeiro, você obtém uma melhor compreensão dos requisitos e regras de negócio antes de iniciar a implementação.

O TDD também incentiva um design de software mais modular e desacoplado, uma vez que os testes são escritos com base nas interfaces e contratos esperados. Isso facilita a aplicação de princípios como a Inversão de Dependência e a escrita de código mais limpo e coeso.

```csharp
// Camada de Testes

namespace MinhaAplicacao.Tests
{
    // Bibliotecas necessárias para escrever os testes
    using Xunit;
    using Moq;

    // Testes unitários para a classe PedidoService
    public class PedidoServiceTests
    {
        [Fact]
        public void CriarPedido_DeveAtualizarStatusCliente()
        {
            // Arrange
            var clienteRepositoryMock = new Mock<IClienteRepository>();
            var pedidoService = new PedidoService(clienteRepositoryMock.Object);

            var pedido = new Pedido { Id = 1, Cliente = new Cliente { Id = 1 } };

            // Act
            pedidoService.CriarPedido(pedido);

            // Assert
            clienteRepositoryMock.Verify(r => r.ObterPorId(1), Times.Once);
            clienteRepositoryMock.Verify(r => r.Salvar(It.IsAny<Cliente>()), Times.Once);
        }

        [Fact]
        public void CancelarPedido_DeveCancelarPedido()
        {
            // Arrange
            var pedidoService = new PedidoService();

            var pedido = new Pedido { Id = 1, Status = "Ativo" };

            // Act
            pedidoService.CancelarPedido(pedido.Id);

            // Assert
            Assert.Equal("Cancelado", pedido.Status);
        }
    }
}
```
Neste exemplo, utilizamos a biblioteca Xunit para escrever os testes unitários. Além disso, utilizamos a biblioteca Moq para criar um objeto mock da interface IClienteRepository e definir o comportamento esperado durante o teste.

Observe que os testes foram escritos primeiro, antes da implementação dos métodos na classe PedidoService. Isso segue o ciclo básico do Test-Driven Development (TDD), onde escrevemos os testes automatizados que falham, implementamos o código necessário para fazer os testes passarem e, em seguida, refatoramos o código para melhorar a qualidade.

Essa abordagem garante que cada funcionalidade seja testada de forma automatizada, aumentando a confiabilidade e a qualidade do código. Além disso, ao escrever os testes primeiro, temos uma melhor compreensão dos requisitos e regras de negócio antes de iniciar a implementação.

## Livro
![Imagem](https://m.media-amazon.com/images/I/51YTqGVOD7L._SY425_.jpg)
