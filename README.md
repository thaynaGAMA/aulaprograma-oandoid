#listade compra1
# aulaprograma-oandoid
import 'package:flutter/material.dart';

void main() {
  runApp(ListaDeComprasApp());
}

class ListaDeComprasApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Lista de Compras',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.green,
        scaffoldBackgroundColor: Colors.grey[100],
      ),
      home: ListaDeComprasPage(),
    );
  }
}

class ListaDeComprasPage extends StatefulWidget {
  @override
  _ListaDeComprasPageState createState() => _ListaDeComprasPageState();
}

class _ListaDeComprasPageState extends State<ListaDeComprasPage> {
  final TextEditingController _controller = TextEditingController();

  List<ItemCompra> _itens = [
    ItemCompra(nome: 'Arroz'),
    ItemCompra(nome: 'Feijão'),
    ItemCompra(nome: 'Óleo'),
    ItemCompra(nome: 'Leite'),
    ItemCompra(nome: 'Sabonete'),
    ItemCompra(nome: 'Papel Higiênico'),
    ItemCompra(nome: 'Pasta de Dente'),
    ItemCompra(nome: 'Pão'),
  ];

  void _adicionarItem(String nome) {
    if (nome.trim().isEmpty) return;
    setState(() {
      _itens.insert(0, ItemCompra(nome: nome));
      _controller.clear();
    });
  }

  void _alternarStatus(int index) {
    setState(() {
      _itens[index].comprado = !_itens[index].comprado;
    });
  }

  void _removerItem(int index) {
    setState(() {
      _itens.removeAt(index);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('🛒 Lista de Compras'),
        centerTitle: true,
      ),
      body: Column(
        children: [
          // Campo de entrada
          Padding(
            padding: const EdgeInsets.symmetric(horizontal: 12.0, vertical: 8),
            child: Row(
              children: [
                Expanded(
                  child: TextField(
                    controller: _controller,
                    decoration: InputDecoration(
                      hintText: 'Adicionar novo item...',
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(12),
                      ),
                      contentPadding: EdgeInsets.symmetric(horizontal: 12),
                    ),
                    onSubmitted: _adicionarItem,
                  ),
                ),
                SizedBox(width: 8),
                ElevatedButton(
                  onPressed: () => _adicionarItem(_controller.text),
                  child: Icon(Icons.add),
                  style: ElevatedButton.styleFrom(
                    shape: CircleBorder(),
                    padding: EdgeInsets.all(12),
                    backgroundColor: Colors.green,
                  ),
                ),
              ],
            ),
          ),

          // Lista de itens
          Expanded(
            child: ListView.builder(
              itemCount: _itens.length,
              itemBuilder: (context, index) {
                final item = _itens[index];
                return Dismissible(
                  key: Key(item.nome + index.toString()),
                  direction: DismissDirection.endToStart,
                  background: Container(
                    color: Colors.red,
                    alignment: Alignment.centerRight,
                    padding: EdgeInsets.symmetric(horizontal: 20),
                    child: Icon(Icons.delete, color: Colors.white),
                  ),
                  onDismissed: (direction) => _removerItem(index),
                  child: ListTile(
                    title: Text(
                      item.nome,
                      style: TextStyle(
                        decoration: item.comprado ? TextDecoration.lineThrough : null,
                        color: item.comprado ? Colors.grey : Colors.black,
                      ),
                    ),
                    trailing: Checkbox(
                      value: item.comprado,
                      onChanged: (_) => _alternarStatus(index),
                    ),
                    onTap: () => _alternarStatus(index),
                  ),
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}

class ItemCompra {
  final String nome;
  bool comprado;

  ItemCompra({required this.nome, this.comprado = false});
}





#listadecompravaloradd


