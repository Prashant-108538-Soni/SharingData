import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

/// A responsive bill card widget that displays bill details such as
/// title, subtitle, amount, status, and action buttons.
/// 
/// This widget scales well across mobile, tablet, and web layouts.
class BillCard extends StatelessWidget {
  final String billTitle;
  final String billId;
  final String svgIconPath;
  final String logoPath;
  final String smartPayStatus;
  final double amount;
  final String scheduledDate;

  const BillCard({
    Key? key,
    required this.billTitle,
    required this.billId,
    required this.svgIconPath,
    required this.logoPath,
    required this.smartPayStatus,
    required this.amount,
    required this.scheduledDate,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // Use LayoutBuilder for responsive sizing
    return LayoutBuilder(
      builder: (context, constraints) {
        return Card(
          margin: const EdgeInsets.all(16),
          shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.circular(16),
          ),
          elevation: 4,
          child: Padding(
            padding: const EdgeInsets.all(16),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [

                /// Top Row: Left icon, Title + ID, Right Logo
                Row(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    // Left: SVG Icon
                    Container(
                      padding: const EdgeInsets.all(8),
                      decoration: BoxDecoration(
                        color: Colors.red.shade50,
                        borderRadius: BorderRadius.circular(12),
                      ),
                      child: SvgPicture.asset(
                        svgIconPath,
                        width: 24,
                        height: 24,
                        placeholderBuilder: (context) => const CircularProgressIndicator(strokeWidth: 1),
                        onPictureError: (error, stackTrace) => const Icon(Icons.error),
                      ),
                    ),

                    const SizedBox(width: 12),

                    // Middle: Title and Subtitle
                    Expanded(
                      child: Column(
                        crossAxisAlignment: CrossAxisAlignment.start,
                        children: [
                          Text(
                            billTitle,
                            style: Theme.of(context).textTheme.titleMedium,
                            overflow: TextOverflow.ellipsis,
                          ),
                          const SizedBox(height: 4),
                          Text(
                            billId,
                            style: Theme.of(context).textTheme.bodySmall,
                          ),
                          const SizedBox(height: 8),
                          // SmartPay Set Indicator
                          Row(
                            children: [
                              const Icon(Icons.check_circle, color: Colors.green, size: 16),
                              const SizedBox(width: 6),
                              Text(
                                smartPayStatus,
                                style: const TextStyle(color: Colors.green, fontWeight: FontWeight.w500),
                              ),
                            ],
                          )
                        ],
                      ),
                    ),

                    const SizedBox(width: 8),

                    // Right: Logo (e.g., Airtel)
                    ClipRRect(
                      borderRadius: BorderRadius.circular(10),
                      child: Container(
                        width: 40,
                        height: 40,
                        color: Colors.white,
                        child: SvgPicture.asset(
                          logoPath,
                          fit: BoxFit.contain,
                          placeholderBuilder: (context) => const Icon(Icons.error),
                        ),
                      ),
                    ),
                  ],
                ),

                const SizedBox(height: 20),

                /// Middle: Amount + Scheduled Date
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceBetween,
                  children: [
                    // Amount
                    Text(
                      '₹ ${amount.toStringAsFixed(2)}',
                      style: const TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
                    ),

                    // Scheduled date pill
                    Container(
                      padding: const EdgeInsets.symmetric(horizontal: 10, vertical: 4),
                      decoration: BoxDecoration(
                        border: Border.all(color: Colors.orange),
                        borderRadius: BorderRadius.circular(20),
                        color: Colors.orange.shade50,
                      ),
                      child: Text(
                        'SCHEDULED: $scheduledDate',
                        style: const TextStyle(color: Colors.orange, fontWeight: FontWeight.w500, fontSize: 12),
                      ),
                    ),
                  ],
                ),

                const SizedBox(height: 20),

                /// Bottom: View Details + 3-dot icon
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceBetween,
                  children: [
                    // View Details Button
                    Expanded(
                      child: OutlinedButton(
                        onPressed: () {},
                        style: OutlinedButton.styleFrom(
                          side: const BorderSide(color: Colors.blue),
                          shape: RoundedRectangleBorder(
                            borderRadius: BorderRadius.circular(10),
                          ),
                        ),
                        child: const Text(
                          'View Details',
                          style: TextStyle(color: Colors.blue),
                        ),
                      ),
                    ),

                    const SizedBox(width: 10),

                    // More Options Icon
                    Container(
                      padding: const EdgeInsets.all(10),
                      decoration: BoxDecoration(
                        border: Border.all(color: Colors.grey.shade400),
                        borderRadius: BorderRadius.circular(12),
                      ),
                      child: const Icon(Icons.more_vert, size: 20),
                    )
                  ],
                ),
              ],
            ),
          ),
        );
      },
    );
  }
}