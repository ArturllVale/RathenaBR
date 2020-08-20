# Importar diretórios

## Para que serve o diretório de importação?

O diretório `import/` fornece uma maneira de você alterar suas configurações sem a necessidade de nem mesmo tocar nos arquivos principais `/conf/` e `/db/`.

Colocando suas entradas personalizadas no diretório `import/` dentro destes dois locais, seus arquivos principais não precisarão ter nenhum conflito resolvido quando você atualizar seu servidor. Você armazena suas alterações e o resto é atualizado com rAthenaBR.

## Como é que isso funciona?
Pense em "importar" como em "substituir". Coloque apenas as configurações que você alterou nos arquivos de importação ou as configurações que você está "substituindo".

Por exemplo, ao configurar um servidor, há sempre algumas configurações que os usuários gostariam de alterar para que o rAthena se adapte às suas necessidades. O exemplo a seguir mostrará como usar o diretório `/ conf / import /` corretamente. (para exemplos de `/ db / import /`, consulte [/db/readme.md](/db/readme.md))

### Login Server
---
Queremos usar senhas MD5 e desabilitar os métodos de criação de contas `_m/_f`.

#### /conf/import/login_conf.txt

	new_account: no
	use_MD5_passwords: yes


### Char Server
---
Queremos mudar o nome do servidor para "Odin".

#### /conf/import/char_conf.txt

	server_name: Odin


### Map Server
---
Queremos ocultar todas as mensagens de erro e adicionar alguns mapas personalizados.

#### /conf/import/map_conf.txt

	// Torna a saída do servidor mais silenciosa, omitindo certos tipos de mensagens:
	// 16: Ocultar mensagens de erro e de erro SQL.
	console_silent: 16
	map: 1@toy
	map: 1@valley
	map: shops


### Inter Server
---
Queremos usar tabelas MySQL em vez de arquivos .txt.

#### /conf/import/inter_conf.txt

	use_sql_db: yes


### Configurações de registro
---
Queremos registrar todos os itens e todas as mensagens de bate-papo.

#### /conf/import/log_conf.txt

	log_filter: 1
	// Log CHAT (Global, Sussurro, Grupo, Guilda, chat principal, Clã) (Nota 3)
	// log_chat: 63 = registra tudo
	log_chat: 63


### Configurações de batalha
---
Queremos mudar a forma como vários mecânimos funcionam. Para qualquer coisa que seria configurada no diretório `/conf/battle/`, ele irá para `import/battle_conf.txt`. Para ajudá-lo a descobrir quais configurações vieram de onde, geralmente é uma boa ideia comentar o nome do arquivo de onde veio a coleção específica de configurações.

#### /conf/import/battle_conf.txt

	// guild.conf
	guild_exp_limit: 90

	// items.conf
	vending_over_max: no
	vending_tax: 100
	weapon_produce_rate: 200
	potion_produce_rate: 200
	produce_item_name_input: 0x03

	// misc.conf
	duel_time_interval: 2
	at_mapflag: yes
	at_monsterignore: yes
	cashshop_show_points: yes
	hide_fav_sell: yes
	// Se o status da caixa de correio é ou não exibido no login.
	// Padrão: 0
	// 0 = Não
	// 1 = Sim
	// 2 = Sim, quando há e-mails não lidos
	mail_show_status: 2

	// monster.conf
	show_mob_info: 3

	// party.conf
	party_hp_mode: 1
	display_party_name: yes

	// pet.conf
	pet_rename: yes

	// player.conf
	max_aspd: 196
	max_third_aspd: 196
	max_extended_aspd: 196
	vip_disp_rate: no

	// status.conf
	debuff_on_logout: 3


Não podemos enfatizar o suficiente o quão útil este sistema é para todos. A maioria dos conflitos git simplesmente desaparecerão se os usuários fizerem uso do sistema `import /`.
