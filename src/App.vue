
<script setup>
import { ref } from 'vue'
import ConteudoEducativo from './components/ConteudoEducativo.vue'

const temaSelecionado = ref(null)
function navegarPara(secao) {
  temaSelecionado.value = null

  setTimeout(() => {
    document.getElementById(secao)?.scrollIntoView({
      behavior: 'smooth'
    })
  }, 50)
}

const temas = [
  {
    titulo: 'Senhas seguras',
    descricao: 'Aprenda a criar e manter senhas fortes para proteger suas contas.',
    texto: 'Utilizar senhas fortes é uma das principais formas de proteger suas informações. Prefira combinações longas, com letras maiúsculas, minúsculas, números e símbolos. Evite informações pessoais e não reutilize a mesma senha em diferentes serviços.'
  },
  {
    titulo: 'Autenticação em dois fatores',
    descricao: 'Conheça uma camada extra de proteção para suas contas digitais.',
    texto: 'A autenticação em dois fatores adiciona uma etapa de verificação ao acesso de uma conta. Mesmo que alguém descubra sua senha, precisará de uma segunda forma de confirmação para entrar.'
  },
  {
    titulo: 'Golpes virtuais',
    descricao: 'Aprenda a identificar phishing e outras tentativas de fraude.',
    texto: 'Golpes virtuais podem chegar por e-mail, mensagens e redes sociais. Desconfie de links suspeitos, ofertas exageradas e pedidos urgentes de informações pessoais. Confira sempre o endereço do remetente e o site antes de fornecer dados.'
  },
  {
    titulo: 'Privacidade e dados',
    descricao: 'Entenda como proteger suas informações pessoais.',
    texto: 'A proteção da privacidade começa com o cuidado ao compartilhar informações. Revise as permissões dos aplicativos, evite divulgar dados pessoais desnecessariamente e utilize configurações de privacidade nas plataformas digitais.'
  },
  {
    titulo: 'Segurança acadêmica',
    descricao: 'Conheça práticas para proteger seus dados no ambiente universitário.',
    texto: 'No ambiente acadêmico, é importante proteger contas institucionais, documentos e trabalhos. Evite acessar suas contas em dispositivos públicos sem cuidado, não compartilhe senhas e sempre encerre a sessão após utilizar computadores compartilhados.'
  },
  {
    titulo: 'Ética digital',
    descricao: 'Aprenda a utilizar a tecnologia de forma consciente e responsável.',
    texto: 'A ética digital envolve respeitar outras pessoas no ambiente virtual, verificar informações antes de compartilhá-las, respeitar direitos autorais e utilizar recursos tecnológicos de maneira responsável.'
  }
]

const perguntas = [
  {
    pergunta: 'Qual destas opções representa uma senha mais segura?',
    alternativas: [
      '12345678',
      'data de nascimento',
      'Casa@2026#Sol',
      'nome123'
    ],
    correta: 2,
    explicacao: 'Senhas fortes combinam letras, números e símbolos, evitando informações fáceis de adivinhar.'
  },
  {
    pergunta: 'Para que serve a autenticação em dois fatores?',
    alternativas: [
      'Deixar a internet mais rápida',
      'Adicionar uma segunda etapa de verificação',
      'Compartilhar a senha com segurança',
      'Eliminar a necessidade de senhas'
    ],
    correta: 1,
    explicacao: 'Ela adiciona uma camada de proteção, exigindo uma segunda confirmação além da senha.'
  },
  {
    pergunta: 'O que fazer ao receber um link suspeito por e-mail?',
    alternativas: [
      'Clicar para verificar',
      'Encaminhar para os colegas',
      'Informar seus dados pessoais',
      'Não clicar e verificar o remetente'
    ],
    correta: 3,
    explicacao: 'Links suspeitos podem levar a páginas falsas. Verifique o remetente e não informe seus dados.'
  },
  {
    pergunta: 'Qual atitude ajuda a proteger sua privacidade?',
    alternativas: [
      'Compartilhar senhas',
      'Publicar todos os dados pessoais',
      'Revisar as permissões dos aplicativos',
      'Usar a mesma senha em todos os sites'
    ],
    correta: 2,
    explicacao: 'Revisar permissões ajuda a controlar quais informações os aplicativos podem acessar.'
  },
  {
    pergunta: 'Qual atitude demonstra ética digital?',
    alternativas: [
      'Compartilhar notícias sem verificar',
      'Respeitar os direitos autorais',
      'Divulgar conversas privadas',
      'Utilizar contas de outras pessoas'
    ],
    correta: 1,
    explicacao: 'A ética digital envolve respeito, responsabilidade e cuidado ao utilizar e compartilhar informações.'
  }
]

const perguntaAtual = ref(0)
const respostaSelecionada = ref(null)
const pontuacao = ref(0)
const questionarioFinalizado = ref(false)
const respostaConfirmada = ref(false)

function responder() {
  if (respostaSelecionada.value === null) return
  if (respostaConfirmada.value) return

  if (respostaSelecionada.value === perguntas[perguntaAtual.value].correta) {
    pontuacao.value++
  }

  respostaConfirmada.value = true
}

function proximaPergunta() {
  if (perguntaAtual.value < perguntas.length - 1) {
    perguntaAtual.value++
    respostaSelecionada.value = null
    respostaConfirmada.value = false
  } else {
    questionarioFinalizado.value = true
  }
}

function reiniciarQuestionario() {
  perguntaAtual.value = 0
  respostaSelecionada.value = null
  pontuacao.value = 0
  questionarioFinalizado.value = false
  respostaConfirmada.value = false
}

</script>

<template>
  <div class="pagina">
    <header class="cabecalho">
      <a href="#" class="logo" @click.prevent="temaSelecionado = null">
  🛡️ Guia Digital
</a>

      <nav>
  <a href="#" @click.prevent="temaSelecionado = null">Início</a>

  <a href="#conteudos" @click.prevent="navegarPara('conteudos')">
    Conteúdos
  </a>

  <a href="#questionario" @click.prevent="navegarPara('questionario')">
    Questionário
  </a>
</nav>
    </header>

    <main v-if="!temaSelecionado">
      <section class="destaque">
        <div>
          <span class="etiqueta">SEGURANÇA E ÉTICA DIGITAL</span>
          <h1>Proteja sua vida digital.</h1>
          <p>
            Aprenda a navegar com mais segurança, proteger seus dados
            e fazer escolhas conscientes no ambiente digital.
          </p>
          <a href="#conteudos" class="botao">Explorar conteúdos</a>
        </div>
      </section>

      <section id="conteudos" class="secao">
        <h2>Aprenda a se proteger</h2>
        <p class="subtitulo">Explore os temas e conheça práticas importantes para sua segurança digital.</p>

        <div class="grade">
          <button
            v-for="(tema, index) in temas"
            :key="tema.titulo"
            class="cartao"
            @click="temaSelecionado = tema"
          >
            <span class="numero">0{{ index + 1 }}</span>
            <h3>{{ tema.titulo }}</h3>
            <p>{{ tema.descricao }}</p>
            <span class="saiba-mais">Saiba mais →</span>
          </button>
        </div>
      </section>

      
<section id="questionario" class="questionario">
  <h2>Teste seus conhecimentos!</h2>
  <p>Responda às perguntas e descubra o quanto aprendeu sobre segurança digital.</p>

  <div class="quiz">
    <div v-if="!questionarioFinalizado">
      <span class="progresso">
        Pergunta {{ perguntaAtual + 1 }} de {{ perguntas.length }}
      </span>

      <div class="barra">
        <div
          class="barra-preenchida"
          :style="{ width: ((perguntaAtual + 1) / perguntas.length * 100) + '%' }"
        ></div>
      </div>

      <h3>{{ perguntas[perguntaAtual].pergunta }}</h3>

      
<div class="alternativas">
  <button
    v-for="(alternativa, index) in perguntas[perguntaAtual].alternativas"
    :key="index"
    class="alternativa"
    :class="{
      selecionada: respostaSelecionada === index,
      correta: respostaConfirmada && index === perguntas[perguntaAtual].correta,
      incorreta: respostaConfirmada && respostaSelecionada === index && index !== perguntas[perguntaAtual].correta
    }"
    :disabled="respostaConfirmada"
    @click="respostaSelecionada = index"
  >
    {{ alternativa }}
  </button>
</div>

<div v-if="respostaConfirmada" class="explicacao">
  <strong>
    {{ respostaSelecionada === perguntas[perguntaAtual].correta
      ? 'Resposta correta!'
      : 'Resposta incorreta!'
    }}
  </strong>
  <p>{{ perguntas[perguntaAtual].explicacao }}</p>
</div>

<button
  v-if="!respostaConfirmada"
  class="botao"
  :disabled="respostaSelecionada === null"
  @click="responder"
>
  Confirmar resposta
</button>

<button
  v-else
  class="botao"
  @click="proximaPergunta"
>
  {{ perguntaAtual === perguntas.length - 1 ? 'Ver resultado' : 'Próxima pergunta' }}
</button>

    </div>

    <div v-else class="resultado">
      <h3>Questionário concluído!</h3>
      <p class="pontuacao">
        Você acertou {{ pontuacao }} de {{ perguntas.length }} perguntas.
      </p>
      <p>{{ pontuacao === perguntas.length
        ? 'Parabéns! Você demonstrou ótimo conhecimento!'
        : 'Continue aprendendo e pratique as dicas do Guia Digital!'
      }}</p>
      <button class="botao" @click="reiniciarQuestionario">
        Refazer questionário
      </button>
    </div>
  </div>
</section>

    </main>

    <ConteudoEducativo
      v-else
      :titulo="temaSelecionado.titulo"
      :descricao="temaSelecionado.descricao"
      :texto="temaSelecionado.texto"
      @voltar="temaSelecionado = null"
    />

    <footer>
      <p>Guia Interativo de Segurança Digital</p>
      <span>Projeto de Extensão – UFMS Digital</span>
    </footer>
  </div>
</template>

<style scoped>
.pagina {
  color: #263b37;
}

.cabecalho {
  min-height: 75px;
  padding: 18px 7%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: white;
  gap: 20px;
}

.logo {
  color: #174c45;
  font-size: 21px;
  font-weight: bold;
  text-decoration: none;
}

nav {
  display: flex;
  gap: 28px;
}

nav a {
  color: #40534e;
  text-decoration: none;
  font-size: 14px;
}

.destaque {
  padding: 90px 10%;
  background: #e6f1ed;
}

.destaque > div {
  max-width: 700px;
}

.etiqueta {
  color: #287665;
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 2px;
}

.destaque h1 {
  margin: 18px 0;
  color: #174c45;
  font-size: clamp(38px, 6vw, 58px);
}

.destaque p {
  max-width: 580px;
  color: #53645e;
  font-size: 18px;
  line-height: 1.7;
}

.botao {
  display: inline-block;
  margin-top: 25px;
  padding: 14px 22px;
  border-radius: 8px;
  background: #287665;
  color: white;
  text-decoration: none;
}

.secao {
  padding: 65px 7%;
}

.secao h2,
.questionario h2 {
  color: #174c45;
  font-size: 30px;
}

.subtitulo {
  margin-top: 10px;
  color: #687770;
}

.grade {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
  margin-top: 30px;
}

.cartao {
  padding: 25px;
  min-height: 210px;
  text-align: left;
  background: white;
  border: 1px solid #dce7e2;
  border-radius: 12px;
  cursor: pointer;
  transition: 0.2s;
}

.cartao:hover {
  transform: translateY(-4px);
  border-color: #287665;
  box-shadow: 0 8px 20px #174c4515;
}

.numero {
  color: #287665;
  font-size: 13px;
  font-weight: bold;
}

.cartao h3 {
  margin: 15px 0 10px;
  color: #174c45;
  font-size: 19px;
}

.cartao p {
  color: #687770;
  line-height: 1.6;
}

.saiba-mais {
  display: inline-block;
  margin-top: 18px;
  color: #287665;
  font-weight: bold;
}

.questionario {
  padding: 55px 7%;
  text-align: center;
  background: #e6f1ed;
}

.questionario p {
  margin-top: 12px;
  color: #53645e;
}

.em-breve {
  font-size: 14px;
}

footer {
  padding: 28px;
  text-align: center;
  background: #174c45;
  color: white;
}

footer span {
  display: block;
  margin-top: 7px;
  font-size: 13px;
  opacity: 0.8;
}

@media (max-width: 768px) {
  .cabecalho {
    flex-direction: column;
  }

  nav {
    gap: 15px;
  }

  .destaque {
    padding: 65px 7%;
  }

  .grade {
    grid-template-columns: 1fr;
  }
}

.quiz {
  max-width: 700px;
  margin: 30px auto 0;
  padding: 30px;
  background: white;
  border: 1px solid #dce7e2;
  border-radius: 14px;
  text-align: left;
}

.progresso {
  color: #287665;
  font-size: 14px;
  font-weight: bold;
}

.barra {
  height: 8px;
  margin: 15px 0 25px;
  overflow: hidden;
  background: #e6f1ed;
  border-radius: 10px;
}

.barra-preenchida {
  height: 100%;
  background: #287665;
  border-radius: 10px;
  transition: width 0.3s;
}

.quiz h3 {
  margin-bottom: 20px;
  color: #174c45;
  font-size: 21px;
}

.alternativas {
  display: grid;
  gap: 12px;
  margin-bottom: 25px;
}

.alternativa {
  padding: 15px;
  border: 1px solid #dce7e2;
  border-radius: 8px;
  background: white;
  color: #40534e;
  text-align: left;
  cursor: pointer;
  font-size: 15px;
}

.alternativa:hover,
.alternativa.selecionada {
  border-color: #287665;
  background: #e6f1ed;
}

.quiz .botao {
  border: none;
  cursor: pointer;
  font-size: 15px;
}

.quiz .botao:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.resultado {
  text-align: center;
}

.resultado .pontuacao {
  margin: 20px 0;
  color: #287665;
  font-size: 24px;
  font-weight: bold;
}


.alternativa:disabled {
  cursor: default;
  opacity: 1;
}

.alternativa.correta {
  border-color: #287665;
  background: #e1f3e9;
  color: #174c45;
}

.alternativa.incorreta {
  border-color: #c65b5b;
  background: #fbeaea;
  color: #8b2929;
}

.explicacao {
  margin-bottom: 22px;
  padding: 18px;
  border-radius: 8px;
  background: #e6f1ed;
  color: #174c45;
  line-height: 1.6;
}

.explicacao p {
  margin-top: 8px;
}

</style>
