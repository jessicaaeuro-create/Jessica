<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

<script>
const supabase = window.supabase.createClient(
  "https://majvmfbdqwjlcizsohwc.supabase.co",
  "COLE_SUA_ANON_KEY_AQUI"
);

// LOGIN
async function login(){
 const email = document.getElementById('email').value;
 const senha = document.getElementById('senha').value;

 const { data, error } = await supabase.auth.signInWithPassword({
   email,
   password: senha
 });

 console.log("LOGIN:", data, error);

 if(error){
   alert(error.message);
 }else{
   alert("ENTROU");
   mostrarApp();
 }
}

// CADASTRO
async function cadastrar(){
 const email = document.getElementById('email').value;
 const senha = document.getElementById('senha').value;

 const { data, error } = await supabase.auth.signUp({
   email,
   password: senha
 });

 console.log("CADASTRO:", data, error);

 if(error){
   alert(error.message);
 }else{
   alert("Conta criada! Agora faz login.");
 }
}

// MOSTRAR APP
function mostrarApp(){
 document.getElementById('login').style.display = 'none';
 document.getElementById('app').style.display = 'block';
}

// AUTO LOGIN (IMPORTANTE)
supabase.auth.getSession().then(({ data }) => {
 if(data.session){
   mostrarApp();
 }
});
</script>
