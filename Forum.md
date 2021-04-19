
# Curso: Spring Boot API REST: Construa uma API

### **Aula 1 - Introdução ao Spring Boot**

- Um resumo da história e evolução do Spring;
- Que, para criar um projeto com Spring Boot, utilizamos o Spring Initialzr, através do site https://start.spring.io;
- Como importar um projeto com Spring Boot na IDE Eclipse;
- Como é o pom.xml de uma aplicação que utiliza o Spring Boot;
- Que, para inicializar o projeto com Spring Boot, devemos utilizar a classe com o método main;
- Que, para criar um controller, utilizamos as anotações @Controller e @RequestMapping.
- Por padrão, o Spring considera que o retorno do método é o nome da página que ele deve carregar, mas ao utilizar a anotação 
@ResponseBody, indicamos que o retorno do método deve ser serializado e devolvido no corpo da resposta.

### **Aula 2 - Publicando Endpoints**

- Sobre a API que desenvolveremos ao longo do curso e sobre as classes de domínio dela;
- Que, para um método no controller não encaminhar a requisição a uma página JSP, ou Thymeleaf, devemos utilizar a anotação @ResponseBody;
- Que o Spring, por padrão, converte os dados no formato JSON, utilizando a biblioteca Jackson;
- Que, para não repetir a anotação @ResponseBody em todos os métodos do controller, devemos utilizar a anotação @RestController;
- Que, para não precisar reiniciar manualmente o servidor a cada alteração feita no código, basta utilizar o módulo Spring Boot DevTools;
- Que não é uma boa prática retornar entidades JPA nos métodos dos controllers, sendo mais indicado retornar classes que seguem o padrão DTO (Data Transfer Object);
- Os principais conceitos sobre o modelo arquitetural REST, como recursos, URIs, verbos HTTP, Representações e comunicação stateless.

### **Aula 3 - Usando Spring Data**

- Para utilizar o JPA no projeto, devemos incluir o módulo Spring Boot Data JPA, que utiliza o Hibernate, por padrão, como sua implementação;
- Para configurar o banco de dados da aplicação, devemos adicionar as propriedades do datasource e do JPA no arquivo src/main/resources/application.properties;
- Para acessar a página de gerenciamento do banco de dados H2, devemos configurar o console do H2 com propriedades no arquivo src/main/resources/application.properties;
- Para mapear as classes de domínio da aplicação como entidade JPA, devemos utilizar as anotações @Entity, @Id, @GeneratedValue, @ManyToOne, @OneToMany e @Enumerated;
- Para que o Spring Boot popule automaticamente o banco de dados da aplicação, devemos criar o arquivo src/main/resources/data.sql;
- Para criar um Repository, devemos criar uma interface, que herda da interface JPARepository do Spring Data JPA;
- Para criar consultas que filtram por atributos da entidade, devemos seguir o padrão de nomenclatura de métodos do Spring, como por exemplo findByCursoNome;
- Para criar manualmente a consulta com JPQL, devemos utilizar a anotação @Query;


### **Aula 4 - Trabalhando com POST**
- Que para evitar repetir a URL em todos os métodos, devemos utilizar a anotação @RequestMapping em cima da classe controller;
- Que para mapear requisições do tipo POST, devemos utilizar a anotação @PostMapping;
- Que para receber dados enviados no corpo da requisição, a boa prática é criar uma classe que também siga o padrão DTO (Data Transfer Object);
- Que a boa prática para métodos que cadastram informações é devolver o código HTTP 201, ao invés do código 200;
- Que para montar uma resposta a ser devolvida ao cliente da API, devemos utilizar a classe ResponseEntity do Spring;
- Que para testar requisições do tipo POST, precisamos utilizar alguma ferramenta de testes de API Rest;
- Como utilizar o Postman para testar uma API Rest;

### **Aula 5 - Validacoes com Bean Validation**

- Para fazer validações das informações enviadas pelos clientes da API, podemos utilizar a especificação Bean Validation, 
com as anotações @NotNull, @NotEmpty, @Size, dentre outras;
- Para o Spring disparar as validações do Bean Validation e devolver um erro 400, caso alguma informação enviada pelo 
cliente esteja inválida, devemos utilizar a anotação @Valid;
- Para interceptar as exceptions que forem lançadas nos métodos das classes controller, devemos criar uma classe anotada 
com @RestControllerAdvice;
- Para tratar os erros de validação do Bean Validation e personalizar o JSON, que será devolvido ao cliente da API, com as 
mensagens de erro, devemos criar um método na classe @RestControllerAdvice e anotá-lo com @ExceptionHandler e @ResponseStatus.

### **Aula 6 - Métodos PUT, DELETE e tratamento de erro**

- Para receber parâmetros dinâmicos no path da URL, devemos utilizar a anotação @PathVariable;
- Para mapear requisições do tipo PUT, devemos utilizar a anotação @PutMapping;
- Para fazer o controle transacional automático, devemos utilizar a anotação @Transactional nos métodos do controller;
- Para mapear requisições do tipo DELETE, devemos utilizar a anotação @DeleteMapping;
- Para tratar o erro 404 na classe controller, devemos utilizar o método findById, ao invés do método getOne, e utilizar a classe ResponseEntity para montar a resposta de not found;
- O método getOne lança uma exception quando o id passado como parâmetro não existir no banco de dados;
- O método findById retorna um objeto Optional<>, que pode ou não conter um objeto.



# Curso: Spring Boot API Rest: Segurança da API, Cache e Monitoramento

### **Aula 1 - Paginação e ordenação de recursos**

- Para realizar paginação com Spring Data JPA, devemos utilizar a interface Pageable;
- Nas classes Repository, os métodos que recebem um pageable como parâmetro retornam objetos do tipo Page<>, ao invés de List<>;
- Para o Spring incluir informações sobre a paginação no JSON de resposta enviado ao cliente da API, devemos alterar o retorno do método do controller de List<> para Page<>;
- Para fazer a ordenação na consulta ao banco de dados, devemos utilizar também a interface Pageable, passando como parâmetro a direção da ordenação, utilizando a classe Direction, e o nome do atributo para ordenar;
- Para receber os parâmetros de ordenação e paginação diretamente nos métodos do controller, devemos habilitar o módulo SpringDataWebSupport, adicionando a anotação @EnableSpringDataWebSupport na classe ForumApplication.

### **Aula 2 - Melhorando desempenho com Spring Cache**
- Para utilizar o módulo de cache do Spring Boot, devemos adicioná-lo como dependência do projeto no arquivo pom.xml;
- Para habilitar o uso de caches na aplicação, devemos adicionar a anotação @EnableCaching na classe ForumApplication;
- Para que o Spring guarde o retorno de um método no cache, devemos anotá-lo com @Cacheable;
- Para o Spring invalidar algum cache após um determinado método ser chamado, devemos anotá-lo com @CacheEvict;
- Devemos utilizar cache apenas para as informações que nunca ou raramente são atualizadas no banco de dados.

### **Aula 3 - Proteção com Spring Security**

- Para utilizar o módulo do Spring Security, devemos adicioná-lo como dependência do projeto no arquivo pom.xml;
- Para habilitar e configurar o controle de autenticação e autorização do projeto, devemos criar uma classe e anotá-la com @Configuration e @EnableWebSecurity;
- Para liberar acesso a algum endpoint da nossa API, devemos chamar o método http.authorizeRequests().antMatchers().permitAll() dentro do método configure(HttpSecurity http), que está na classe SecurityConfigurations;
- O método anyRequest().authenticated() indica ao Spring Security para bloquear todos os endpoints que não foram liberados anteriormente com o método permitAll();
- Para implementar o controle de autenticação na API, devemos implementar a interface UserDetails na classe Usuario e também implementar a interface GrantedAuthority na classe Perfil;
- Para o Spring Security gerar automaticamente um formulário de login, devemos chamar o método and().formLogin(), dentro do método configure(HttpSecurity http), que está na classe SecurityConfigurations;
- A lógica de autenticação, que consulta o usuário no banco de dados, deve implementar a interface UserDetailsService;
- Devemos indicar ao Spring Security qual o algoritmo de hashing de senha que utilizaremos na API, chamando o método passwordEncoder(), dentro do método configure(AuthenticationManagerBuilder auth), que está na classe SecurityConfigurations.


### **Aula 4 - Gerando token com JWT**

- Em uma API Rest, não é uma boa prática utilizar autenticação com o uso de session;
- Uma das maneiras de fazer autenticação stateless é utilizando tokens JWT (Json Web Token);
- Para utilizar JWT na API, devemos adicionar a dependência da biblioteca jjwt no arquivo pom.xml do projeto;
- Para configurar a autenticação stateless no Spring Security, devemos utilizar o método sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);
- Para disparar manualmente o processo de autenticação no Spring Security, devemos utilizar a classe AuthenticationManager;
- Para poder injetar o AuthenticationManager no controller, devemos criar um método anotado com @Bean, na classe SecurityConfigurations, que retorna uma chamada ao método super.authenticationManager();
- Para criar o token JWT, devemos utilizar a classe Jwts;
- O token tem um período de expiração, que pode ser definida no arquivo application.properties;
- Para injetar uma propriedade do arquivo application.properties, devemos utilizar a anotação @Value.


### **Aula 05 - Autenticação via JWT**

- Para enviar o token JWT na requisição, é necessário adicionar o cabeçalho Authorization, passando como valor Bearer token;
- Para criar um filtro no Spring, devemos criar uma classe que herda da classe OncePerRequestFilter;
- Para recuperar o token JWT da requisição no filter, devemos chamar o método request.getHeader("Authorization");
- Para habilitar o filtro no Spring Security, devemos chamar o método and().addFilterBefore(new AutenticacaoViaTokenFilter(), UsernamePasswordAuthenticationFilter.class);
- Para indicar ao Spring Security que o cliente está autenticado, devemos utilizar a classe SecurityContextHolder, chamando o método SecurityContextHolder.getContext().setAuthentication(authentication).
- Vimos que precisamos criar um filtro, que vai conter a lógica de recuperar o token do cabeçalho Authorization, validá-lo e autenticar o cliente. Porem nao existe anotacao para registrar o filtro, ele
deve ser registrado via método addFilterBefore, na classe SecurityConfigurations.
- Por que não é possível fazer injeção de dependências com a anotação @Autowired na classe AutenticacaoViaTokenFilter? 
Por que ela não é um bean gerenciado pelo Spring. O filtro foi instanciado manualmente por nós, na classe SecurityConfigurations e portanto o Spring não consegue realizar injeção de dependências via @Autowired.
- Vimos que foi necessário indicar ao Spring que o cliente está autenticado. Por que essa autenticação foi feita com a classe SecurityContextHolder e não com a AuthenticationManager?
Porque a classe AuthenticationManager dispara o processo de autenticação via username/password. A classe AuthenticationManager deve ser utilizada apenas na lógica de autenticação via username/password, para a geração do token.

### **Aula 06 - Monitoramento com Spring Boot Actuator**

- Para adicionar o Spring Boot Actuator no projeto, devemos adicioná-lo como uma dependência no arquivo pom.xml;
- Para acessar as informações disponibilizadas pelo Actuator, devemos entrar no endereço http://localhost:8080/actuator;
- Para liberar acesso ao Actuator no Spring Security, devemos chamar o método .antMatchers(HttpMethod.GET, "/actuator/**");
- Para que o Actuator exponha mais informações sobre a API, devemos adicionar as propriedades management.endpoint.health.show-details=always e management.endpoints.web.exposure.include=* no arquivo application.properties;
- Para utilizar o Spring Boot Admin, devemos criar um projeto Spring Boot e adicionar nele os módulos spring-boot-starter-web e spring-boot-admin-server;
- Para trocar a porta na qual o servidor do Spring Boot Admin rodará, devemos adicionar a propriedade server.port=8081 no arquivo application.properties;
- Para o Spring Boot Admin conseguir monitorar a nossa API, devemos adicionar no projeto da API o módulo spring-boot-admin-client e também adicionar a propriedade spring.boot.admin.client.url=http://localhost:8081 no arquivo application.properties;
- Para acessar a interface gráfica do Spring Boot Admin, devemos entrar no endereço http://localhost:8081.

### **Aula 07 - Documentação da API com Swagger**

- Para documentar a nossa API Rest, podemos utilizar o Swagger, com o módulo SpringFox Swagger;
- Para utilizar o SpringFox Swagger na API, devemos adicionar suas dependências no arquivo pom.xml;
- Para habilitar o Swagger na API, devemos adicionar a anotação @EnableSwagger2 na classe ForumApplication;
- As configurações do Swagger devem ser feitas criando-se uma classe chamada SwaggerConfigurations e adicionando nela a anotação @Configuration;
- Para configurar quais endpoints e pacotes da API o Swagger deve gerar a documentação, devemos criar um método anotado com @Bean, que devolve um objeto do tipo Docket;
- Para acessar a documentação da API, devemos entrar no endereço http://localhost:8080/swagger-ui.html;
- Para liberar acesso ao Swagger no Spring Security, devemos chamar o seguinte método web.ignoring().antMatchers("/**.html", "/v2/api-docs", "/webjars/**", "/configuration/**", "/swagger-resources/**"), dentro do método void configure(WebSecurity web), que está na classe SecurityConfigurations.

# Curso 3 - Spring Boot e Teste: Profiles, Testes e Deploy

### **Aula 01 - Mais Segurança**

- Para atualizar a versão do Spring Boot na aplicação, basta alterar a tag <version> da tag <parent>, no arquivo pom.xml.  
-É importante ler as release notes das novas versões do Spring Boot, para identificar possíveis quebras de compatibilidades ao atualizar a aplicação.  
- É possível restringir o acesso a determinados endpoints da aplicação, de acordo com o perfil do usuário autenticado, utilizando o método hasRole(“NOME_DO_ROLE”) nas configurações de segurança da aplicação.  

### **Aula 02 - Profiles**

- Profiles devem ser utilizados para separar as configurações de cada tipo de ambiente, tais como desenvolvimento, testes e produção.  
- A anotação @Profile serve para indicar ao Spring que determinada classe deve ser carregada apenas quando determinados profiles estiverem ativos.  
- É possível alterar o profile ativo da aplicação por meio do parâmetro -Dspring.profiles.active.  
- Ao não definir um profile para a aplicação, o Spring considera que o profile ativo dela e o profile de nome default.  


### **03 - Testes automatizados**
- É possível escrever testes automatizados de classes que são beans do Spring, como Controllers e Repositories.  
- É possível utilizar injeção de dependências nas classes de testes automatizados.  
- A anotação @SpringBootTest deve ser utilizada nas classes de testes automatizados para que o Spring inicialize o servidor e disponibilize os beans da aplicação.  
- Ao testar uma interface Repository devemos, preferencialmente, utilizar a anotação @DataJpaTest.  
- Por padrão, os testes automatizados dos repositories utilizam um banco de dados em memória, como o h2.  
- É possível utilizar outro banco de dados para os testes automatizados, utilizando a anotação @AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE).  
- É possível forçar um profile específico para os testes automatizados com a utilização da anotação @ActiveProfiles.
Para conseguir injetar o MockMvc devemos anotar a classe de teste com @AutoConfigureMockMvc.  

### **04 - Deploy**

- O build da aplicação é realizado via maven, com o comando mvn clean package.  
- Ao realizar o build, por padrão será criado um arquivo .jar.  
- É possível passar parâmetros para as configurações da aplicação via variáveis de ambiente.  
- É possível alterar o build para criar um arquivo .war, para deploy em servidores de aplicações.  
- Rodar o projeto no terminal: java -jar -DFORUM_DATABASE_URL=jdbc:h2:mem:alura-forum -DFORUM_DATABASE_USERNAME=sa -DFORUM_DATABASE_PASSWORD= -DFORUM_JWT_SECRET=123456 forum.jar
- Deploy da app como war:

no pom.xml adicionar:
 <packaging>war</packaging>

 e

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>

na classe main do projeto

- extender da classe SpringBootServletInitializer
- sobrescrever  o metodo configure:

@Override
protected SpringApplicationBuilder configure(SpringApplicationBuiilder builder){
    return builder.sources(ForumApplication.class);
}


### **05. Deploy com Docker e na nuvem**

- É possível utilizar o Docker para criação de imagens e de containers para aplicações que utilizam Java com Spring Boot.  
- Devemos criar um arquivo Dockerfile no diretório raiz da aplicação, para ensinar ao Docker como deve ser gerada a imagem dela.  
- É possível passar as variáveis de ambiente utilizadas pela aplicação para o container Docker.  
- É possível realizar o deploy de aplicações Java com Spring Boot em ambientes Cloud, como o Heroku.  
- Cada provedor Cloud pode exigir diferentes configurações adicionais a serem realizadas na aplicação, para que ela seja executada sem nenhum tipo de problema.  
- Gerar imagem no docker: docker build -t alura/forum .  
- Iniciar o container: docker run -p 8080:8080 -e SPRING_PROFILES_ACTIVE='prod' -e FORUM_DATABASE_URL='jdbc:h2:mem:alura-forum' -e FORUM_DATABASE_USERNAME='sa' -e FORUM_DATABASE_PASSWORD=' ' -e FORUM_JWT_SECRET='123456' alura/forum


