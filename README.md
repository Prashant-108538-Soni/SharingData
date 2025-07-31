import 'package:flutter/material.dart';

void main() { runApp(const MaterialApp( debugShowCheckedModeBanner: false, home: EventCardScreen(), )); }

class EventCardScreen extends StatelessWidget { const EventCardScreen({super.key});

@override Widget build(BuildContext context) { final Map<String, List<Widget>> eventsByDate = { '04 October\nToday': [ buildEventCard( context, title: "Mom's Phone Bill", subtitle: "9989090909 | Mobile Postpaid", amount: "₹885.00", paymentStatus: "PAID", statusColor: Colors.blue, buttonLabel: "View Details", ), buildEventCard( context, title: "Personal Loan", subtitle: "3456765544 | Loan EMI", amount: "₹6,885.00", paymentStatus: "OVERDUE", statusColor: Colors.red, buttonLabel: "Pay Now", buttonColor: Colors.blue, buttonTextColor: Colors.white, ), buildEventCard( context, title: "Infinia Credit Card", subtitle: "3456765544 | Credit Card Bill", amount: "₹12,943.00", paymentStatus: "PAID", statusColor: Colors.blue, buttonLabel: "View Details", ), ], '08 October\nSun': [ buildEventCard( context, title: "Mom's Phone Bill", subtitle: "9909890989", amount: "₹6885.00", paymentStatus: "SCHEDULED: 17 SEP", statusColor: Colors.orange, buttonLabel: "View Details", ), ], };

return Scaffold(
  backgroundColor: Colors.grey.shade100,
  body: CustomScrollView(
    slivers: [
      for (final entry in eventsByDate.entries) ...[
        SliverPersistentHeader(
          pinned: true,
          delegate: StickyDateHeader(entry.key),
        ),
        SliverList(
          delegate: SliverChildListDelegate(
            entry.value
                .map((e) => Padding(
                      padding: const EdgeInsets.symmetric(
                          horizontal: 12, vertical: 8),
                      child: e,
                    ))
                .toList(),
          ),
        )
      ]
    ],
  ),
);

} }

class StickyDateHeader extends SliverPersistentHeaderDelegate { final String date;

StickyDateHeader(this.date);

@override Widget build( BuildContext context, double shrinkOffset, bool overlapsContent) { return Container( color: Colors.grey.shade100, alignment: Alignment.centerLeft, padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 8), child: Text( date, style: const TextStyle( fontWeight: FontWeight.bold, fontSize: 13, ), ), ); }

@override double get maxExtent => 40;

@override double get minExtent => 40;

@override bool shouldRebuild(covariant StickyDateHeader oldDelegate) { return oldDelegate.date != date; } }

Widget buildEventCard( BuildContext context, { required String title, required String subtitle, required String amount, required String paymentStatus, required Color statusColor, required String buttonLabel, Color buttonColor = Colors.white, Color buttonTextColor = Colors.blue, }) { return Container( decoration: BoxDecoration( color: Colors.white, borderRadius: BorderRadius.circular(12), border: Border.all(color: Colors.grey.shade300), ), padding: const EdgeInsets.all(12), child: Column( crossAxisAlignment: CrossAxisAlignment.start, children: [ Row( crossAxisAlignment: CrossAxisAlignment.start, children: [ // Icon placeholder Container( width: 36, height: 36, decoration: BoxDecoration( color: Colors.grey.shade300, shape: BoxShape.circle, ), child: const Icon(Icons.receipt_long_rounded, size: 18), ), const SizedBox(width: 12), Expanded( child: Column( crossAxisAlignment: CrossAxisAlignment.start, children: [ Text(title, style: const TextStyle( fontWeight: FontWeight.w600, fontSize: 14)), const SizedBox(height: 2), Text(subtitle, style: TextStyle(color: Colors.grey.shade600, fontSize: 12)), const SizedBox(height: 4), Row( children: const [ Icon(Icons.verified, size: 14, color: Colors.green), SizedBox(width: 4), Text( 'SmartPay Set', style: TextStyle( fontSize: 11, fontWeight: FontWeight.w500, color: Colors.green), ) ], ) ], ), ) ], ), const SizedBox(height: 14), Row( children: [ Text( amount, style: const TextStyle(fontSize: 15, fontWeight: FontWeight.bold), ), const SizedBox(width: 10), Container( padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 2), decoration: BoxDecoration( borderRadius: BorderRadius.circular(12), color: statusColor.withOpacity(0.1), border: Border.all(color: statusColor), ), child: Text( paymentStatus, style: TextStyle( fontSize: 10, fontWeight: FontWeight.w500, color: statusColor), ), ), const Spacer(), ElevatedButton( style: ElevatedButton.styleFrom( backgroundColor: buttonColor, foregroundColor: buttonTextColor, side: BorderSide(color: buttonTextColor), shape: RoundedRectangleBorder( borderRadius: BorderRadius.circular(8)), padding: const EdgeInsets.symmetric(horizontal: 16, vertical: 10), ), onPressed: () {}, child: Text( buttonLabel, style: TextStyle( fontSize: 12, fontWeight: FontWeight.w600, color: buttonTextColor), ), ), const SizedBox(width: 6), const Icon(Icons.more_vert, size: 18) ], ) ], ), ); }

