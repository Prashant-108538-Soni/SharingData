import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sticky Date Cards',
      debugShowCheckedModeBanner: false,
      home: StickyDateCardScreen(),
    );
  }
}

class StickyDateCardScreen extends StatelessWidget {
  final Map<String, List<String>> data = {
    '04 October': [
      'Mom’s Phone Bill',
      'Personal Loan',
      'Infinia Credit Card',
      'Electricity Bill',
      'Netflix Subscription',
    ],
    '05 October': [
      'Credit Card EMI',
      'Grocery Payment',
      'Amazon Order',
      'Phone Recharge',
      'School Fees',
      'Health Insurance',
    ],
    '08 October': [
      'Mom’s Phone Bill',
    ],
  };

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sticky Date Card List'),
        backgroundColor: Colors.deepPurple,
      ),
      body: CustomScrollView(
        slivers: data.entries.map((entry) {
          return SliverStickyDateSection(date: entry.key, items: entry.value);
        }).toList(),
      ),
    );
  }
}

class SliverStickyDateSection extends StatelessWidget {
  final String date;
  final List<String> items;

  const SliverStickyDateSection({required this.date, required this.items});

  @override
  Widget build(BuildContext context) {
    return SliverList(
      delegate: SliverChildListDelegate.fixed(
        [
          StickyHeader(date: date),
          ...items.map((item) => PaymentCard(title: item)).toList(),
        ],
      ),
    );
  }
}

class StickyHeader extends StatelessWidget {
  final String date;

  const StickyHeader({required this.date});

  @override
  Widget build(BuildContext context) {
    return Container(
      color: Colors.grey[200],
      padding: const EdgeInsets.symmetric(horizontal: 16, vertical: 12),
      alignment: Alignment.centerLeft,
      child: Text(
        date,
        style: TextStyle(
          fontSize: 18,
          fontWeight: FontWeight.bold,
          color: Colors.deepPurple,
        ),
      ),
    );
  }
}

class PaymentCard extends StatelessWidget {
  final String title;

  const PaymentCard({required this.title});

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 6),
      child: Card(
        elevation: 4,
        shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
        child: ListTile(
          contentPadding: const EdgeInsets.all(16),
          title: Text(
            title,
            style: TextStyle(fontWeight: FontWeight.w600),
          ),
          subtitle: Text('Details for $title'),
          trailing: ElevatedButton(
            onPressed: () {},
            child: Text('View'),
          ),
        ),
      ),
    );
  }
}