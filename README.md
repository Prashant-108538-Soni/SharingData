import 'package:flutter/material.dart';
import 'package:flutter_sticky_header/flutter_sticky_header.dart';

/// A widget that displays grouped event cards with sticky date headers.
/// Uses [flutter_sticky_header] package to pin headers during scroll.
class StickyActionSection extends StatelessWidget {
  /// A map where the key is a date string and value is a list of event card widgets.
  final Map<String, List<Widget>> groupedEventCards;

  const StickyActionSection({
    super.key,
    required this.groupedEventCards,
  });

  @override
  Widget build(BuildContext context) {
    final List<Widget> slivers = [];

    groupedEventCards.forEach((String date, List<Widget> cards) {
      slivers.add(
        SliverStickyHeader(
          header: _StickyDateHeader(date: date),
          sliver: SliverList(
            delegate: SliverChildBuilderDelegate(
              (context, index) => Padding(
                padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 8),
                child: cards[index],
              ),
              childCount: cards.length,
            ),
          ),
        ),
      );
    });

    return CustomScrollView(
      slivers: slivers,
    );
  }
}

class _StickyDateHeader extends StatelessWidget {
  final String date;

  const _StickyDateHeader({required this.date});

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 40,
      color: Colors.grey.shade200,
      padding: const EdgeInsets.symmetric(horizontal: 16),
      alignment: Alignment.centerLeft,
      child: Text(
        date,
        style: const TextStyle(fontWeight: FontWeight.bold, fontSize: 14),
      ),
    );
  }
}



import 'package:flutter/material.dart';
import 'sticky_action_section.dart'; // Your file
import 'compact_event_card.dart'; // Your event card widget

class EventScreen extends StatelessWidget {
  const EventScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Upcoming Bills')),
      body: StickyActionSection(
        groupedEventCards: {
          "04 October": List.generate(3, (index) => _buildMockCard(context, "Mom's Phone Bill")),
          "08 October": List.generate(2, (index) => _buildMockCard(context, "Infinia Credit Card")),
        },
      ),
    );
  }

  /// Mock card generator using your existing CompactEventCard
  Widget _buildMockCard(BuildContext context, String title) {
    return CompactEventCard(
      prefixIconPath: 'assets/icons/bill.svg',
      suffixIconPath: 'assets/icons/hdfc_logo.svg',
      descriptionText: 'SmartPay Set',
      descriptionIconPath: 'assets/icons/smartpay.svg',
      amount: 6885.00,
      paymentStatus: 'SCHEDULED',
      paymentStatusBackgroundColor: Colors.orange.shade50,
      paymentStatusTextColor: Colors.orange,
      title: title,
      prefixIconColor: Colors.blue.shade100,
      subTitle: '9988090989 | Mobile Postpaid',
      eventDateWithLabel: 'SCHEDULED: 17 SEP',
      actionItems: [
        EventCardActionItem(title: 'View Details', onTap: () {}),
      ],
      menuButtonIconPath: 'assets/icons/more.svg',
    );
  }
}