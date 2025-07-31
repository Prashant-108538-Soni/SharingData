import 'package:flutter/material.dart';

/// A customizable widget to display the status of a bill payment.
/// This widget presents a status text within a container that features a
/// colored border and background, both derived from the provided color parameters.
/// The text is automatically converted to uppercase and styled with a bold font.
/// This widget provides internal horizontal and vertical padding for its content
/// and defines its width based on the content's size and parent constraints.

class PaymentStatus extends StatelessWidget {
  /// The status string to be displayed (e.g., "Paid", "Pending", "Failed").
  /// This text will be converted to uppercase.
  final String status;

  /// The color used for the text and the border of the container.
  final Color borderTextColor;

  /// The background color of the status container.
  final Color backgroundColor;

  /// Creates a BillPaymentStatus widget.
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
        style: TextStyle(color: borderTextColor, fontWeight: FontWeight.bold),
        textAlign: TextAlign.center, // Center the text within the container
      ),
    );
  }
}
