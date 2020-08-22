# Import diretórios

## Para que serve o diretório import?

O diretório `import/` fornece uma maneira de você alterar suas configurações sem a necessidade de nem mesmo tocar nos arquivos principais `/conf/` e `/db/`.

Colocando suas entradas personalizadas no diretório `import/` dentro destes dois locais, seus arquivos principais não precisarão ter nenhum conflito resolvido quando você atualizar seu servidor. Você armazena suas alterações e o resto é atualizado com rAthenaBR.

## Como é que isso funciona?

Pense em "import" como em "substituir". Coloque apenas as configurações que você alterou nos arquivos de importação ou as configurações que você está "substituindo".

Por exemplo, ao configurar um servidor, há sempre algumas configurações que os usuários gostariam de alterar para que o rAthenaBR se adapte às suas necessidades. O exemplo a seguir mostrará como usar o diretório `/db/import/` corretamente. (para exemplos de `/conf/import/`, consulte [/conf/readme.md](/conf/readme.md))

### Conquistas
---
We want to add our own custom achievement that can be given to a player via an NPC Script and another that we can give to our GMs.

#### /db/import/achievement_db.yml


    Conquistas:
      - ID: 280000
        Group: "AG_GOAL_ACHIEVE"
        Name: "Emperio"
        Reward:
          TitleID: 1035
        Score: 50
      - ID: 280001
        Group: "AG_GOAL_ACHIEVE"
        Name: "Staff"
        Reward:
          TitleID: 1036
        Score: 50


### Instâncias
---
Queremos adicionar nossa própria instância de habitação personalizada.

#### /db/import/instance_db.yml

	- Id: 35
	    Name: Home
        IdleTimeOut: 900
        Enter:
          Map: 1@home
          X: 24
          Y: 6
        AdditionalMaps:
          - Map: 2@home
          - Map: 3@home


### Mob Alias
---
Queremos dar a um mob personalizado um sprite de jogador Novato.

#### /db/import/mob_avail.txt

    // Structure of Database:
    // MobID,SpriteID{,Equipment}
    3850,0


### Mapas Personalizados
---
Queremos adicionar nossos próprios mapas personalizados. Para isso, precisamos adicionar nossos nomes de mapa a `import/map_index.txt` e então ao arquivo` import/map_cache.dat` para o Map Server carregar.

#### /db/import/map_index.txt

    1@home	1250
    2@home
    3@home
    ev_has
    shops
    prt_pvp


### Restrições ao comércio de itens
---
Queremos garantir que itens específicos não possam ser negociados, vendidos, descartados, colocados em armazenamento, etc.

#### /db/import/item_trade.txt

// Legenda para o campo 'TradeMask' (bitmask):
    // 1 - o item não pode ser descartado
    // 2 - o item não pode ser comercializado (nem vendido)
    // 4 - o parceiro casado pode anular a restrição 2
    // 8 - o item não pode ser vendido para npcs
    // 16 - o item não pode ser colocado no carrinho
    // 32 - o item não pode ser colocado no armazenamento
    // 64 - o item não pode ser colocado no armazenamento da guilda
    // 128 - o item não pode ser anexado ao correio
    // 256 - o item não pode ser leiloado
    // Valor definitivo total = 511
    34000.511.100 // Old Green Box
    34001.511.100 // Chaves da casa
    34002.511.100 // Jornal de Reputação


### Missões personalizadas
---
Queremos adicionar nossas próprias missões personalizadas ao quest_db.

#### /db/import/quest_db.txt

    // Quest ID,Time Limit,Target1,Val1,Target2,Val2,Target3,Val3,MobID1,NameID1,Rate1,MobID2,NameID2,Rate2,MobID3,NameID3,Rate3,Quest Title
    89001,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"Quest de Reputação"
    89002,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,"Quest de Reputação"



Não podemos enfatizar o suficiente o quão útil este sistema é para todos. A maioria dos conflitos git simplesmente desaparecerão se os usuários fizerem uso do sistema `import/`.
