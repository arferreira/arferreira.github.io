---
layout: post
title: Um pouco de lógica com Ruby
---
Hoje vou falar um pouco de lógica com Ruby codando um pequeno jogo de adivinhação.
Há algum tempo quando retornei a estudar Ruby puramente falando encontrei este exemplo em um livro muito bacana da Casa do Código, achei bem interessante para iniciar os posts aqui do blog com este artigo, principalmente para quem busca iniciar na linguagem, acredito que antes de visualizar nosso querido framework Rails, devemos nos dedicar muito com Ruby.
Irei partir do princípio de que quem chegou aqui já possui o Ruby instalado. Qualquer dúvida basta entrar em contato comigo por algum dos canais expostos aqui no blog.

Inicialmente o código irá escolher um número aleatório e o usuário deverá adivinha-lo em 10 chances.

Entre as chances o usuário receberá mensagens se o número informado é maior ou menor que o do sistema. 

Criaremos um arquivo chamado "maior_menor.rb" para começarmos o nosso jogo.

Inicio o software com um método chamado welcome, nele pego uma informação sobre o usuário:

{% highlight rb %}
def welcome
	puts "Bem-vindo ao jogo da adivinhação."
	puts "\n\n"
	puts "Qual é o seu nome?"
	name = gets
	puts "\n\n"
	puts "Começaremos o jogo para você, #{name}"
end

{% endhighlight %}

Pronto, agora criarei um método chamado sort, que fará o sorteio de um número aleatório para o jogador e irá devolver a uma variável o número escolhido. Essa variável recebe um número randômico da class Random e para ele passo um range entre 0 e 200. Lembrando que sempre o ruby retornará a última linha de um método.

{% highlight rb %}
def sort
	puts "\n\n"
	puts "Escolhendo um número secreto entre 0 e 200..."
	number_secret = Random.rand(0..200)
	puts "Escolhido.. Que tal adivinhar hoje nosso número secreto.?"
	number_secret
end

{% endhighlight %}

Agora eu irei criar um método para pegar o chute do usuário do jogo, este método irá receber um array com os chutes já realizados, a tentativa e o limite de tentativas possíveis para o usuário. E ao final retorno o chute do usuário.

{% highlight rb %}
def get_number kicks, attempt, limit
	puts "\n\n\n\n"
	puts "Tentativa #{attempt.to_s} de #{limit.to_s}"
	puts "Chutes até agora:  #{kicks.to_s}"
	puts "Escolha um número: "
	kick = gets
	kick = kick.to_i
	puts  "Será que você acertou? Você escolheu o número: #{kick.to_s}"
	kick
end
{% endhighlight %}

Agora preciso verificar se o chute realizado pelo usuário corresponde ao número secreto escolhido pelo sistema, para isso crio um método, que recebe dois parâmetros (chute e número secreto), verifico se o chute é igual ao número secreto, se for envio uma mensagem ao usuário e saio do método com "true", caso não eu aindo verifico se o número é maior ou menor para aproximar as chances dos usuários acertarem.

{% highlight rb %}
def verify kick, number_secret

hit =  kick == number_secret

	if hit
        	puts "Parabéns, você acertou :)"
	        return true
	else
        	puts "Humm... você errou :("
		larger = number_secret > kick
        	if larger
        		puts "O número secreto é maior."
       		 else
        		puts "O número secreto é menor."
        	end
		return false
	end
end
{% endhighlight %}

Pronto, agora o programa já tem todas as suas ações definidas, agora irei organiza-lo e unir todos os métodos no arquivo maior_menor.rb:

{% highlight rb %}
def welcome
	puts "Bem-vindo ao jogo da adivinhação."
	puts "\n\n"
	puts "Qual é o seu nome?"
	name = gets
	puts "\n\n"
	puts "Começaremos o jogo para você, #{name}"
end



def sort
	puts "\n\n"
	puts "Escolhendo um número secreto entre 0 e 200..."
	number_secret = Random.rand(0..200)
	puts "Escolhido.. Que tal adivinhar hoje nosso número secreto.?"
	number_secret
end



def get_number kicks, attempt, limit
	puts "\n\n\n\n"
	puts "Tentativa #{attempt.to_s} de #{limit.to_s}"
	puts "Chutes até agora:  #{kicks.to_s}"
	puts "Escolha um número: "
	kick = gets
	kick = kick.to_i
	puts  "Será que você acertou? Você escolheu o número: #{kick.to_s}"
	kick
end


def verify kick, number_secret

hit =  kick == number_secret

	if hit
        	puts "Parabéns, você acertou :)"
	        return true
	else
        	puts "Humm... você errou :("
		larger = number_secret > kick
        	if larger
        		puts "O número secreto é maior."
       		 else
        		puts "O número secreto é menor."
        	end
		return false
	end
end
{% endhighlight %}

Feito isso, preciso chamar os métodos e começar a trabalhar com eles.

{% highlight rb %}
welcome


number_secret = sort


limit = 10

kicks = []

for attempt in 1..limit

	kick = get_number kicks, attempt, limit

	kicks << kick

	break  if verify kick, number_secret

end
{% endhighlight %}

Chamo o método welcome para dar as boas vindas ao usuário e pegar o seu nome, chamo o método responsável por sortear um número para o sistema, defino o limite de tentativas para 10, crio o array de chutes e faço um laço para realizar as 10 tentativas, enviando ao método "verify" o chute e o número secreto, e quando o mesmo retorna uma condição verdadeira, saímos do jogo.

Agora o arquivo "maior_menor.rb" completo:

{% highlight rb %}
def welcome
	puts "Bem-vindo ao jogo da adivinhação."
	puts "\n\n"
	puts "Qual é o seu nome?"
	name = gets
	puts "\n\n"
	puts "Começaremos o jogo para você, #{name}"
end

def sort
	puts "\n\n"
	puts "Escolhendo um número secreto entre 0 e 200..."
	number_secret = Random.rand(0..200)
	puts "Escolhido.. Que tal adivinhar hoje nosso número secreto.?"
	number_secret
end

def get_number kicks, attempt, limit
	puts "\n\n\n\n"
	puts "Tentativa #{attempt.to_s} de #{limit.to_s}"
	puts "Chutes até agora:  #{kicks.to_s}"
	puts "Escolha um número: "
	kick = gets
	kick = kick.to_i
	puts  "Será que você acertou? Você escolheu o número: #{kick.to_s}"
	kick
end


def verify kick, number_secret

hit =  kick == number_secret

	if hit
        	puts "Parabéns, você acertou :)"
	        return true
	else
        	puts "Humm... você errou :("
		larger = number_secret > kick
        	if larger
        		puts "O número secreto é maior."
       		 else
        		puts "O número secreto é menor."
        	end
		return false
	end
end


welcome

number_secret = sort

limit = 10

kicks = []

for attempt in 1..limit
	kick = get_number kicks, attempt, limit
	kicks << kick
	break  if verify kick, number_secret
end
{% endhighlight %}

> Basta ir ao terminal e executar o arquivo.: $: ruby maior_menor.rb

Jogo maior_menor no Github: https://github.com/arferreira/maior_ou_menor

Espero que este post ajude alguém como me ajudou ao iniciar com ruby e estudar novamente a sintaxe da linguagem e os seus conceitos. É isso ai e até a próxima.