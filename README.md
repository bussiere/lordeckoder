# Legends of Runeterra Deckcode Decoder - lordeckoder

Golang package to decode Legends of Runeterra deckstring to useful data inspired by [LoRDeckCodes](https://github.com/RiotGames/LoRDeckCodes).

# Installation

```bash
go get github.com/MarekSalgovic/lordeckoder
```



# Usage

Decodes deckcode string to deck struct. For more details see [format](https://github.com/RiotGames/LoRDeckCodes#process).
```go
func main(){
	dc := "CEBACAIDFIDQCAQGBAIRULBRHEBAEAICAILAGAIDBQKBWAQBAEBASBIBAMMSGKZWG4"
	// deckcode, format and version number
	// use lordeckoder.Decode(dc) for default (currently 1,1)
	deck, err := lordeckoder.Decode(dc, 1,1)
	
	if err != nil{
		log.Fatalln(err)
	}
	fmt.Println(deck)
	//{[{01NX042 3} {01IO006 3} {01IO008 3} {01IO017 3} {01IO026 3}
	//  {01IO044 3} {01IO049 3} {01IO057 3} {01IO002 2} {01IO022 2}
	//  {01NX012 2} {01NX020 2} {01NX027 2} {01IO009 1} {01NX025 1}
	//  {01NX035 1} {01NX043 1} {01NX054 1} {01NX055 1}]}
	fmt.Println(deck.Cards[0].CardCode.Number)
	//42
	fmt.Println(deck.Cards[0].CardCode.Faction)
	//3
	fmt.Println(lordeckoder.FactionIdToString(deck.Cards[0].CardCode.Faction))
	//NX
	fmt.Println(deck.Cards[0].CardCode)
	//01NX042
}

```

Available structs:

```go
type Deck struct {
	Cards []Card
}

type Card struct {
	CardCode CardCode
	Count    int
}

type CardCode struct {
	Set     int
	Faction int
	Number  int
}

```

