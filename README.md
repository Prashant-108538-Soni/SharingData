import 'package:flutter/material.dart';

void main() {
  runApp(const MaterialApp(home: StickyDateScreen()));
}

class StickyDateScreen extends StatelessWidget {
  const StickyDateScreen({super.key});

  // Sample data
  Map<String, List<String>> get groupedEvents => {
        '04 October': [
          'Mom\'s Phone Bill',
          'Personal Loan',
          'Infinia Credit Card',
        ],
        '08 October': ['Mom\'s Phone Bill'],
      };

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.grey[100],
      body: CustomScrollView(
        slivers: groupedEvents.entries.map((entry) {
          final date = entry.key;
          final events = entry.value;

          return SliverStickySection(
            date: date,
            children: events
                .map((title) => Padding(
                      padding: const EdgeInsets.only(bottom: 12),
                      child: EventCard(title: title),
                    ))
                .toList(),
          );
        }).toList(),
      ),
    );
  }
}

class SliverStickySection extends StatelessWidget {
  final String date;
  final List<Widget> children;

  const SliverStickySection({
    super.key,
    required this.date,
    required this.children,
  });

  @override
  Widget build(BuildContext context) {
    return SliverList.list(
      children: [
        _StickyRow(date: date),
        ...children,
      ],
    );
  }
}

class _StickyRow extends StatelessWidget {
  final String date;

  const _StickyRow({required this.date});

  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(
      builder: (context, _) {
        return Row(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Container(
              width: 120,
              padding: const EdgeInsets.only(left: 12, top: 16),
              alignment: Alignment.topLeft,
              child: Text(
                date,
                style: const TextStyle(
                  fontWeight: FontWeight.bold,
                  color: Colors.black87,
                ),
              ),
            ),
            const SizedBox(width: 10),
            Expanded(
              child: Column(
                children: const [],
              ),
            ),
          ],
        );
      },
    );
  }
}

class EventCard extends StatelessWidget {
  final String title;

  const EventCard({super.key, required this.title});

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: const EdgeInsets.only(right: 16),
      padding: const EdgeInsets.all(16),
      decoration: BoxDecoration(
        color: Colors.white,
        border: Border.all(color: Colors.grey.shade400),
        borderRadius: BorderRadius.circular(12),
      ),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Text(title,
              style: const TextStyle(
                  fontWeight: FontWeight.bold, fontSize: 16)),
          const SizedBox(height: 8),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              const Text("₹ 885.00",
                  style: TextStyle(fontWeight: FontWeight.w600)),
              OutlinedButton(
                onPressed: () {},
                child: const Text("View Details"),
              )
            ],
          )
        ],
      ),
    );
  }
}