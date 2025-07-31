import 'package:flutter/material.dart';

/// A compact label widget to display the payment status of a bill.
///
/// Shows uppercase status text inside a container with custom
/// background and border color. Commonly used for statuses like
/// "PAID", "PENDING", or "FAILED".
class PaymentStatus extends StatelessWidget {
  /// Status label to display (e.g., "Paid", "Failed").
  /// Rendered in uppercase.
  final String status;

  /// Color for the border and text.
  final Color borderTextColor;

  /// Background color of the container.
  final Color backgroundColor;

  const PaymentStatus({
    super.key,
    required this.status,
    required this.borderTextColor,
    required this.backgroundColor,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: const EdgeInsets.symmetric(vertical: 2, horizontal: 8),
      decoration: BoxDecoration(
        color: backgroundColor,
        border: Border.all(color: borderTextColor, width: 1.0),
        borderRadius: BorderRadius.circular(8.0),
      ),
      child: Text(
        status.toUpperCase(),
        style: TextStyle(
          color: borderTextColor,
          fontWeight: FontWeight.bold,
        ),
        textAlign: TextAlign.center,
      ),
    );
  }
}