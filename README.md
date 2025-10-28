# Atividade-Pr-tica-Implementa-o-de-Criptografia-RSA-em-Rust
I. Princípios Matemáticos Fundamentais
A segurança e o funcionamento do RSA dependem de conceitos robustos da teoria dos números. O RSA é baseado no problema matemático da dificuldade de fatorar números grandes.
1. Aritmética Modular
A aritmética modular é o pilar do RSA. Ela lida com restos de divisões e define a operação essencial: a≡b(modn) (lê-se "a é congruente a b módulo n").
• É fundamental saber que a exponenciação modular (a 
k
 )modn pode ser calculada eficientemente.
2. Números Primos e o Problema da Fatoração
O RSA exige a geração de dois números primos grandes e distintos, p e q.
• O módulo n é calculado como o produto desses primos: n=p×q.
• O Problema da Fatoração afirma que, dado n, encontrar p e q é computacionalmente difícil para números grandes. Esta dificuldade é a base da segurança do RSA.
3. Função Totiente de Euler (φ(n))
Esta função é crucial para gerar o expoente privado.
• φ(n) é a quantidade de números menores que n que são coprimos com n.
• Para o RSA, φ(n) é calculado a partir dos primos secretos: φ(n)=(p−1)×(q−1).
• Atenção: O valor de φ(n) deve ser mantido em segredo.
4. Teorema de Euler e Inverso Modular
O teorema de Euler garante que o processo de descriptografia funciona matematicamente.
• Um corolário essencial afirma que: a 
(k×φ(n)+1)
 ≡a(modn).
• A chave privada d é o inverso modular da chave pública e módulo φ(n), o que significa que e×d≡1(modφ(n)). Este valor é calculado usando o Algoritmo Euclidiano Estendido.

--------------------------------------------------------------------------------
II. Funcionamento do Algoritmo RSA Passo-a-Passo
O funcionamento do RSA é dividido em duas fases principais: Geração de Chaves e Uso das Chaves (Criptografia/Descriptografia).
Fase 1: Geração de Chaves
1. Escolha de Primos: Gerar p e q (primos grandes, de tamanhos similares).
2. Cálculo do Módulo: n=p×q (Este é o módulo público).
3. Cálculo do Totiente: φ(n)=(p−1)×(q−1).
4. Escolha do Expoente Público (e): Escolher e tal que 1<e<φ(n). O valor mais comum, devido à eficiência, é e=65537.
5. Cálculo do Expoente Privado (d): Calcular d, o inverso modular de e módulo φ(n).
• Resultado: A Chave Pública é (n,e), e a Chave Privada é (n,d).
Fase 2: Uso das Chaves
Criptografia (Usando a Chave Pública (n,e)): Para criptografar uma mensagem m (representada como um número menor que n): 
c=m 
e
 modn
 Onde c é o texto criptografado.
Descriptografia (Usando a Chave Privada (n,d)): Para descriptografar o texto cifrado c: 
m=c 
d
 modn
 O resultado m é a mensagem original.
Otimização Crucial: Tanto a criptografia quanto a descriptografia dependem da Exponenciação Modular Rápida (Square-and-Multiply) para viabilizar o RSA, pois esta evita o cálculo de números gigantescos, garantindo uma complexidade eficiente de O(log exp).

--------------------------------------------------------------------------------
III. Aplicações Práticas em Segurança da Informação
O RSA é amplamente adotado e é a base de muitos protocolos modernos.
1. Versatilidade e Adotabilidade
• Bidirecional: O RSA não apenas criptografa, mas também permite a criação de assinaturas digitais.
• Adoção Ampla: É usado como base para protocolos de segurança cruciais como HTTPS e SSH.
2. Uso Típico (Criptografia Híbrida)
Embora sólido, o RSA é cerca de 1000 vezes mais lento que algoritmos de criptografia simétrica (como o AES). Por essa razão:
• Uso Recomendado: O RSA é tipicamente usado para troca de chaves simétricas. Em um sistema híbrido, o RSA criptografa uma chave simétrica pequena, e essa chave simétrica é usada para criptografar os dados grandes.
3. Requisitos de Segurança
A segurança do RSA está ligada ao tamanho de n.
• Tamanhos de Chave: Chaves de 1024 bits são consideradas quebradas. Atualmente, o tamanho mínimo seguro recomendado é 2048 bits (que oferece equivalência simétrica de 112 bits), sendo 3072 bits o tamanho recomendado para 2025.
• Contramedidas Cruciais: Para implementação em produção, é obrigatório usar padding seguro (como OAEP para criptografia e PSS para assinatura digital) e bibliotecas testadas (como OpenSSL), além de proteções contra ataques de canal lateral (timing attacks).
4. Limitações Futuras
Apesar de sua maturidade, o RSA enfrenta uma limitação fundamental:
• Ameaça Quântica: O RSA é vulnerável ao Algoritmo de Shor, que pode quebrá-lo em tempo polinomial quando computadores quânticos suficientemente poderosos (com cerca de 4096 qubits lógicos) forem implementados (estimativa atual: 10-20 anos). A contramedida futura é a migração para a criptografia pós-quântica.
Conclusão: O RSA prova que "a matemática pode ser tanto elegante quanto prática, fornecendo segurança através da beleza dos números primos". Seu fundamento matemático sólido e versatilidade garantiram sua posição como base da segurança digital por décadas, sendo essencial para a troca segura de chaves e assinaturas digitais
