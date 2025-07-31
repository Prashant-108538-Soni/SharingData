import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:hdfc_flutter_widgets/event_card/common/smart_pay_status.dart';

/// A reusable widget that displays a primary detail row consisting of:
/// - A leading SVG icon inside a colored circular background
/// - A title (main label)
/// - A short description
/// - A smart pay status widget that shows a status with an icon and text
///
/// This widget is designed to be used in event or transaction cards
/// where a quick summary of an item needs to be shown in a structured layout.
class PrimaryDetail extends StatelessWidget {
  /// Path to the leading SVG asset (e.g., "assets/icons/phone_bill.svg")
  final String prefixIconPath;

  /// Background color of the circular container that wraps the icon
  final Color prefixIconBackgroundColor;

  /// The main title or event name to be shown (e.g., "Mom's Phone Bill")
  final String title;

  /// The subtitle or additional supporting text (currently unused in the UI)
  final String subtitle;

  /// Description text shown below the title
  final String descriptionText;

  /// Path to the SVG asset used inside SmartPayStatus widget
  final String descriptionIconPath;

  const PrimaryDetail({
    super.key,
    required this.title,
    required this.prefixIconPath,
    required this.prefixIconBackgroundColor,
    required this.descriptionIconPath,
    required this.descriptionText,
    required this.subtitle,
  });

  @override
  Widget build(BuildContext context) {
    return Row(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        // Leading circular icon
        Container(
          padding: const EdgeInsets.all(8),
          decoration: BoxDecoration(
            shape: BoxShape.circle,
            color: prefixIconBackgroundColor,
          ),
          alignment: Alignment.center,
          child: SizedBox(
            width: 24,
            height: 24,
            child: SvgPicture.asset(
              prefixIconPath,
              // Fallback icon if asset fails to load
              placeholderBuilder: (BuildContext context) =>
                  const Icon(Icons.error_outline, color: Colors.red),
            ),
          ),
        ),

        const SizedBox(width: 12),

        // Title, description, and status section
        Expanded(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              // Title text
              Text(
                title,
                style: const TextStyle(
                  fontWeight: FontWeight.w600,
                  color: Colors.black87,
                ),
                overflow: TextOverflow.ellipsis,
                maxLines: 2,
              ),

              const SizedBox(height: 4),

              // Description text
              Text(
                descriptionText,
                style: TextStyle(color: Colors.grey.shade800),
                overflow: TextOverflow.ellipsis,
                maxLines: 2,
              ),

              const SizedBox(height: 20),

              // Status row (icon + label)
              SmartPayStatus(
                svgPath: descriptionIconPath,
                text: descriptionText,
              ),
            ],
          ),
        ),
      ],
    );
  }
}